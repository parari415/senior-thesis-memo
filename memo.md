#### バイナリファイル作成
* fallocate -l [サイズ] [ファイル名]
```
fallocate -l 100M testdate
```

#### 暗号化
* <実行ファイル名> -k <鍵ファイル> -e|-d -i <入力ファイル> -o <出力ファイル>
```
./speck -k key_128.key -e -i testdate -o encrypted.bin
```

#### 復号
* <実行ファイル名> -k <鍵ファイル> -e|-d -i <入力ファイル> -o <出力ファイル>
```
./speck -k key_128.key -d -i encrypted.bin -o decrypted.bin
```

#### 計測
* 暗号化・復号コマンドの前に/usr/bin/time -vをつける
```
/usr/bin/time -v ./speck -k key_128.key -e -i testdate -o encrypted.bin
```

#### 指定回数繰り返す
* for i in {1..<繰り返し回数>}; do
  echo "===== Run $i =====" >> <ログファイル名>
  <コマンド> 2>> <ログファイル名>
done
```
for i in {1..10}; do
  echo "===== Run $i =====" >> speck_100m.log
  /usr/bin/time -v ./speck -k key_128.key -e -i testdate100m -o ciphertext.bin 2>> speck_100m.log
done
```
```
for i in {1..10}; do
  echo "===== Run $i =====" >> d_speck_10m.log
  /usr/bin/time -v ./speck -k key_128.key -d -i ciphertext.bin -o decrypted_$i.bin 2>> d_speck_10m.log
done
```

#### 抽出
* grep "<検索したい文字列>" <検索対象ファイル>
```
grep "Elapsed" result.log
```