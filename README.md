# AI training
How to learn AI Service develepment.

# Contents
1. ブラウザから使ってみる
1. プログラムから使ってみる

# ブラウザから使ってみる
## 画像に映っているのは何？
この画像はフルーツボールです。バナナ、青りんご、オレンジなど色々なフルーツが盛られています。  
このように人が見て、画像に含まれるものを列挙することは、比較的簡単なことです。  
![fruitbowl.jpg](docs/img/fruitbowl.jpg)

## では、ヒトではなく機械に画像が認識できるのか
機械は、「モノの名前」と「スコア」で画像に何が映っているのかを認識する。  
スコアが高いほどが一致率が高いことを示す。
```
機械が認識した例

モノの名前 ： スコア(%)

規定食 (食品):0.579%
食物:0.579%
果実:0.826%
バナナ:0.532%
ゴールデン・デリシャス:0.508%
生食用リンゴ:0.641%
リンゴ:0.654%
ナシ状果:0.669%
グラニー・スミス:0.5%
オリーブ色:0.943%
レモン・イエロー (色):0.898%
```

## ブラウザから画像認識サービスを呼び出す  
以下のリンクは画像認識サービスAPIのリンクで、指定された画像URL（フルーツボール）より指定した画像を認識し、結果をJSONで返します。IBMクラウドが提供している画像認識APIを使用しています。  

https://gateway-a.watsonplatform.net/visual-recognition/api/v3/classify?api_key=befb491ae8c532e1db72518f6da8088bb2bd1b52&url=https://namickey.github.io/ai_train_2018/img/fruitbowl.jpg&version=2016-05-20

## 画像認識サービスAPIのパラメータ
上記でクリックした画像認識サービスのURLを説明します。
```
https://gateway-a.watsonplatform.net/visual-recognition/api/v3/classify?
api_key=befb491ae8c532e1db72518f6da8088bb2bd1b52&
url=https://namickey.github.io/ai_train_2018/img/fruitbowl.jpg&
version=2016-05-20
※読みやすいように改行を入れているので注意。

* api_key：APIの利用に必要なキー。このキーは認証や回数集計や課金に利用される。  
* url：任意の画像URL。ここで指定された画像の認識が行われる。  
* version：指定された固定バージョンを入力する。  
```

## 別画像のURLを指定する
* 試してみたい画像URLをコピーする。  
  必ずインターネット上の画像URLであること。  
* コピーした画像URLを、APIパラメータの２番目（url）と置き換える。  
* ブラウザに完成したAPIのURLを入力する。  

例えば、ここに「チキン」の画像がある。  
https://namickey.github.io/ai_train_2018/img/chicken.jpg

この画像を使い画像認識サービスを呼び出すには、以下のURLのようになる。  
https://gateway-a.watsonplatform.net/visual-recognition/api/v3/classify?api_key=befb491ae8c532e1db72518f6da8088bb2bd1b52&url=https://namickey.github.io/ai_train_2018/img/chicken.jpg&version=2016-05-20

「チキン」の画像  
![chicken.jpg](docs/img/chicken.jpg)



## 【やってみよう】IBMクラウドの無料アカウント取得
自分のアカウントのapi_keyを使って、画像認識サービスを呼び出してみよう。  
* IBMクラウドの無料アカウントに登録する。  
  ※クレジットカード不要  
  ※10日又は1ヶ月放置すると自動的にアカウント停止となる。  
* カタログから、画像認識サービスの申込みをする。  
* 画像認識サービスで、api_keyの発行を行う。  
* 発行されたapi_keyを使って、画像認識サービスを呼び出す。  

# プログラムから画像認識サービスを呼び出す
## curl実行
```
curl 'https://gateway-a.watsonplatform.net/visual-recognition/api/v3/classify?api_key=befb491ae8c532e1db72518f6da8088bb2bd1b52&url=https://namickey.github.io/ai_train_2018/img/chicken.jpg&version=2016-05-20'
```

## JAVA実行
```
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.IOException;
import java.net.URL;
import java.net.HttpURLConnection;

public class Sample {
    public static void main(String[] args) throws IOException {
        URL url = new URL("https://gateway-a.watsonplatform.net/visual-recognition/api/v3/classify?api_key=befb491ae8c532e1db72518f6da8088bb2bd1b52&url=https://namickey.github.io/ai_train_2018/img/chicken.jpg&version=2016-05-20");
        HttpURLConnection con = (HttpURLConnection) url.openConnection();
        con.setRequestProperty("Accept-Language", "ja");
        try (BufferedReader reader = (con.getResponseCode() >= 400 ? new BufferedReader(new InputStreamReader(con.getErrorStream())) : new BufferedReader(new InputStreamReader(con.getInputStream())))) {
            reader.lines().forEach(System.out::println);
        }
    }
}
```

## Python実行
```
import requests
url='https://gateway-a.watsonplatform.net/visual-recognition/api/v3/classify?api_key=befb491ae8c532e1db72518f6da8088bb2bd1b52&url=https://namickey.github.io/ai_train_2018/img/chicken.jpg&version=2016-05-20'
headers = {'Accept-Language': 'ja'}
response = requests.get(url, headers=headers)
print(response)
```
