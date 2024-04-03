# Bookmarklets for Amazon and Kindle

このDocumentでは、
- Amazon Book Info Extractor: Amazonの書籍情報を抽出する
- Kindle Highlights Extractor: Kindleのハイライトデータを抽出する

これらのブックマークレットの使用方法について説明します。

## Bookmarkletsとは？
Bookmarklets（ブックマークレット）は、ウェブブラウザで使用できる小さなプログラムです。これをブラウザのブックマークバーに保存しておくことで、特定のタスクをワンクリックで実行できるようになります。JavaScriptで書かれており、ウェブページの表示や挙動をカスタマイズするのに便利です。

## 1. Amazon Book Info Extractor

### 機能
このブックマークレットは、Amazonの書籍ページにアクセスした際に、書籍のタイトル、著者、ISBN番号などの情報を簡単に抽出し、表示するために使用します。

### 使用方法
1. 以下のコード、またはAmazonBookInfoExtractor.txtの内容をコピーし、ブックマークとしてブラウザに追加します。ブックマークを追加し、URL欄にコードを貼り付けて保存してください。
   ```javascript
   javascript:(function(){let details='',title='',author='',imageURL='',category='Motivational Business Management';const detailsDiv=document.querySelector('#detailBullets_feature_div');if(detailsDiv){detailsDiv.querySelectorAll('ul.detail-bullet-list > li').forEach(item=>{const labelElement=item.querySelector('.a-text-bold');if(labelElement&&!labelElement.textContent.includes('Customer Reviews')&&!labelElement.textContent.includes('Dimensions')){const value=labelElement.nextElementSibling?labelElement.nextElementSibling.textContent.trim().split('(')[0].trim():'';details+='\n'+labelElement.textContent.trim()+': '+value;}});}else{details='Details not found';}title=document.querySelector('#productTitle, #ebooksProductTitle')?.innerText.trim()||'Title not found';author=Array.from(document.querySelectorAll('.author a.a-link-normal')).map(e=>e.innerText.trim()).join(', ')||'Author not found';imageURL=document.querySelector('img#landingImage')?.src||'Image URL not found';const yaml=%60---\ntag: Book\ntitle: "${title}"\nauthor: "${author}"\nConsumed: false\nReview: false\ncategory: ${category}\nRating: \nurl: ![](${imageURL})\n---\n[[${author}]]%60;const textarea=document.createElement("textarea");textarea.value=yaml;document.body.appendChild(textarea);textarea.select();document.execCommand('copy');document.body.removeChild(textarea);alert('Information copied to clipboard:\n'+yaml);})();
   ```

2. Amazonの任意の書籍ページを開きます。

3. ブラウザのブックマークバーに保存した「Amazon Book Info Extractor」をクリックします。

4. 書籍の詳細情報が以下のようにポップアップで表示され、コピーされます。
    ```markdown
    ---
    tag: Book
    title: "LIFE PACKING 2020 未来を生きるためのモノと知恵 (NEXTRAVELER BOOKS)"
    author: "高城剛"
    Consumed: false
    Review: false
    category: Motivational Business Management
    Rating: 
    url: ![](https://m.media-amazon.com/images/I/81uaqEKx5SL._SY522_.jpg)
    ---
    [[高城剛]]
    ```

## 2. Kindle Highlights Extractor

### 機能
このブックマークレットは、Kindleでハイライトしたテキストデータを抽出し、簡単にコピーできるようにするために使用します。
- 赤色のハイライト: 見出し「###」
- 青色のハイライト: 本文

### 使用方法
1. 以下のコード、またはKindleHighlightsExtractor.txtの内容をコピーし、ブックマークとしてブラウザに追加します。ブックマークを追加し、URL欄にコードを貼り付けて保存してください。
   ```javascript
   javascript:(function(){const e=document.querySelectorAll('span#annotationHighlightHeader'),t=document.querySelectorAll('div[id^="highlight-"]');let n=[];if(t.length===e.length){for(let l=0;l<t.length;l++){let a=t[l],i=a.textContent.trim();a.classList.contains('kp-notebook-highlight-pink')?i=%60### ${i}%60:a.classList.contains('kp-notebook-highlight-blue')||(i=%60${i}%60),n.push(i)}}let d=n.join('\n');const r=document.createElement('textarea');r.style.position='fixed',r.style.top=0,r.style.left=0,r.style.width='100%',r.style.height='100%',r.style.zIndex=2147483647,r.textContent=d,document.body.innerHTML='',document.body.appendChild(r),r.select();})();
   ```

2. [Kindle Library](https://read.amazon.co.jp/kindle-library)から、ノートとハイライトを表示するページにアクセスし、ハイライトしたい本を選択します。

3. ブラウザのブックマークバーに保存した「Kindle Highlights Extractor」をクリックします。

4. ハイライトしたテキストデータが表示され、以下のような形式でコピーされます。
    ```markdown
    ### このハイライトは赤色です。
    このハイライトは青色です。
    このハイライトは青色です。
    ### このハイライトは赤色です。
    このハイライトは青色です。
    このハイライトは青色です。
    ```


## 注意事項
- これらのブックマークレットは、ブラウザのJavaScriptが有効になっている必要があります。
- 特定のウェブページやブラウザのセキュリティ設定によっては、ブックマークレットが期待通りに動作しないことがあります。
- ブックマークレットの使用は、ご自身の責任で行ってください。公式のツールやアプリとは異なり、サポートや保証が提供されるものではありません。
