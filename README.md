# AJACSオンライン8 「ウェブツールを使ってゲノム編集の標的サイトを検索する」

プラチナバイオ株式会社 兼
広島大学 ゲノム編集イノベーションセンター   
[中前和恭](https://researchmap.jp/knakamae)  
nakamae@pt-bio.com
2021年8月19日（木）
AJACSオンライン8

----

これは統合データベース講習会 AJACSオンライン8「ウェブツールを使ってゲノム編集の標的サイトを検索する」の講習資料です。  
講習会全体のプログラムは[こちら](https://biosciencedbc.jp/event/ajacs/ajacs89.html)です。
© 2021 中前 和恭, [CC-BY-4.0](https://creativecommons.org/licenses/by/4.0/deed.ja)

----
## 自己紹介
- [中前 和恭](https://researchmap.jp/knakamae)  
  - プラチナバイオ主任研究員 兼 広島大学ゲノム編集イノベーションセンター研究員、ゲノム編集実験・解析・ツール開発
  - 開発ソフト
    - [PITCh designer](https://www.mls.sci.hiroshima-u.ac.jp/smg/PITChdesigner/index.html)
    - MaChIAto
    - Genome Editing Cloud (プラチナバイオ・広島大学・凸版印刷による共同開発中)
      - プレスリリース（https://www.toppan.co.jp/news/2021/03/newsrelease210305_1.html）
  - 教育歴
    - 
  - [researchmap](https://researchmap.jp/knakamae)
  - [Twitter](https://twitter.com/kazuki_nakamae)

----
## 概要

本講習では、だれでも自由に使うことができるウェブツールを活用して、適切なゲノム編集を行うための標的検索とその考え方について学びます。
また、さまざまな目的に特化した標的選定やゲノム編集後の解析に活用できるツールについても学びます。

----

## 講習の流れ
今回の講習では、以下の内容について説明します。

- 1章. ゲノム編集を使ってノックアウトのための標的を設計する
  - CRISPR-Cas9を使ったノックアウト設計
    - CRISPRdirect
    - CRISPROR
  - CRISPR-Cas9を使ったノックアウト結果の予測
    - MMEJ-predictor
    - InDelphi

- 2章. より詳しいゲノム編集のためにデータベース・ツールを知る
  - ゲノム編集ウェブツール一覧
  - Cas9によるノックイン設計ツール：PITCh designer 2.0
  - TALENによるノックアウト設計ツール：TAL Effector Nucleotide Targeter 2.0
  - Base Editorによる塩基編集設計ツール：BE-Designer
  - Base Editorによる塩基編集予測ツール：BE-Hive
  - Prime Editorによる小規模編集設計ツール：PrimeDesign
  - Cas13によるRNA編集設計ツール：Cas13design
  - ウイルスに対するゲノム編集設計ツール：COMBAT crRNA Repository
  - サンガーシーケンスデータを使った変異分析ツール：TIDE
  - アンプリコンシーケンシングデータを使った変異分析ツール：CRISPResso2
  - UCSC genome browserを使ったCas9標的の検索
  - ガイドRNA先行研究データベース：dbGuide
  - MMEJサイト検索データベース：MHcut Browser
- 3章. ゲノム編集情報の安全な設計・解析・管理ツール
  - GGGenome（+パッケージ版）によるオフターゲット検索
  - Genome Editing Cloudの紹介

## 講義に際して
- 今回はウェブツールを紹介しますが、同時にアクセスするとサイトにつながりにくくなる可能性があります
    - 資料を見ながら自力で進められそうな方はどんどん先に進めていっても大丈夫です。
    - タイミングをずらして実行するとうまく接続できる場合があります。

----

#### 受講前アンケートにご協力いただき、ありがとうございます (回答数 XXX)(XXX時点)

|統合TVを知っていますか?|人数|割合|
|:--|--:|:--:|
|知らない|21 名|13 %|
|知っている|137 名|87 %|

---
|自分で実験して得た、数十〜数千の遺伝子からなる<br>「遺伝子リスト」(例: 発現差のあった遺伝子など) を持っていますか?|人数|割合|
|:--|--:|:--:|
|既に持っている|61 名|40.7 %|
|これから実験をする・したい|29 名|19.3 %|
|公共データを活用する・したい|47 名|31.3 %|
|大規模発現解析の予定はない|13 名|8.7 %|
---



## ゲノム編集とは？

s

## 1章. ゲノム編集を使ってノックアウトのための標的を設計する

### CRISPR-Cas9を使ったノックアウト設計

#### ノックアウトについて

  - 遺伝子の機能を消失させるノックアウト法にはさまざまな方法が知られています。一種類のCRISPR-Cas9を使ったランダム変異導入や複数のCRISPR-Cas9を使ったラージデリーション導入、TALENによる変異導入、そして古典的なノックインによるノックアウトなどが知られています。今回の標的選択では現在最もシンプルな方法として知られている一種類のCRISPR-Cas9を使ったランダム変異導入を考えてみます。
  - ノックアウトを行う位置に関してですが、単純に遺伝子を破壊したいという場合であれば開始コドンの直下のExon領域をターゲットにして、ゲノム編集でフレームシフトを発生させる方法が一般的です。これによって中途半端な翻訳産物を生み出すことなく、多くの場合において遺伝子の発現を完全に抑えることが可能です。
  - 標的を選ぶ際にはできる限りしっかりとアノテーションがついた情報を参照するようにしましょう。本資料末尾にある0章ではNCBIから遺伝子情報をダウンロードしていますが、こうしたものでは一つの遺伝子に対して複数種のアイソフォームが割り当てられているものがあります。完全にノックアウトを行いたい場合はなるべく全てのアイソフォームに重複するExon領域でゲノム編集のターゲットを選択するようにしてください。
  - ノックアウトの結果、事前情報からでは想定できなかった翻訳産物が出現するケースもあります。ゲノム配列の確認とともに、qPCR、ddPCR、ウェスタンブロット等で発現レベルを確認することも重要です。

#### [CRISPRdirect](https://crispr.dbcls.jp)
- CRISPR-Cas9標的を検索できるウェブツール。特にオフターゲット作用を考慮した検索が可能。
    - [https://crispr.dbcls.jp](https://crispr.dbcls.jp)
    - [論文](https://doi.org/10.1093/bioinformatics/btu743)
    - [紹介動画 - 統合TV](https://doi.org/10.7875/togotv.2014.025)
    トップページ
    ![](/images/1a.png)      
    検索にヒットした標的候補一覧表
    ![](/images/1b.png)
    標的候補の位置関係
    ![](/images/1c.png)
    データ出力も可能です。
    ![](/images/1d.png)
    ![](/images/1e.png)
- 標的候補一覧表の見方
  ![](/images/1f.png)
  - "position"
    - "start - end"はターゲットの位置になります。
    - "+-"はゲノムリファレンス上でどちらのstrand属するかを指します。
  - "target sequence"
    - "target seqeunce"が標的とする配列です。 四角で囲まれているのがPAM結合サイトであり、それ以外の部分はガイドRNAがもつprotospacer配列を指します。
  - "sequence information"
    - "GC% of 20mer"や"Tm of 20mer"はprotospacer配列のGC%・Tm値を指します。
    - "TTTT in 20mer"はprotospacer配列に4連続するTがあるかどうかを指します。こうした配列はプロモータによっては転写終結シグナルとなるため使用を避けた方がよいです。
    - "restriction sites"はそこに制限酵素サイトがあるかどうかを示します。ゲノム編集の解析をする場合には編集した箇所で作用する制限酵素を使って変異導入の有無を電気泳動で確認する方法があります（RFLP法）。ここで示されている制限酵素はそういった検証に利用可能です。
  - "number of target sites"
    - "20mer+PAM"はPAM結合サイトとプロトスペーサー配列のゲノム上での特異性を指します。
      - 1の場合はゲノム上に1つしかないということを表します。
      - それ以上の場合は、目的でない結合箇所（オフターゲットサイト）がゲノム上に数カ所あるということになります。
      - 0の場合はゲノム上に存在しないことを表します。成熟mRNA配列などから配列を取得した場合ではExonのつなぎ目領域でこのような結果になることがあります。こうしたものは基本的にターゲティングできません。
    - "12mer+PAM"や"8mer+PAM"はPAM結合サイトとプロトスペーサー配列の3´末端から12bp, 8bpのゲノム上での特異性を指します。SpCas9の特異性は位置依存的であることが知られており、3´側に位置するほど特異性が高くなる傾向があります。3´末端から12bp, 8bpの領域で一致するオフターゲットサイトが大量にある場合はゲノムに対して意図しない変異導入を大量に起こしてしまう可能性が高く、ゲノム編集の標的として適切とはいえません。
    - "detail"をクリックすると、検索にヒットした標的配列あるいはオフターゲットサイトがゲノム上のどのあたりに存在するか参照することが可能です。
      - "≤1 mismatch/gap"または"≤2 mismatch/gap"をクリックすることで、ミスマッチ・ギャップを含むオフターゲットサイトも表示することもできます。
      ![](/images/1g.png)

----

#### 【使用例】CRISPRdirectを使って、ノックアウトのための標的を設計する

1. 検索配列を入力します。
![]()

2. 配列はSnapGene Viewerからドラッグ->コピーで取得します。今回は開始コドンから159bpを取得します。

入力配列：
>MYOG
atggagctgtatgagacatccccctacttctaccaggaaccccgcttctatgatggggaaaactacctgcctgtccacctccagggcttcgaaccaccaggctacgagcggacggagctcaccctgagccccgaggccccagggccccttgaggacaag
![]()
![]()

3. Cas9のPAM配列を入力します。今回は最も一般的なSpCas9の"NGG"とします。
PAM配列：NGG
![]()

4. 特異性を確認するゲノムを指定します。今回は最新のヒトゲノムリファレンスである"Human (Homo sapiens) genome, GRCh38/hg38 (Dec, 2013)"とします。
ゲノム：Human (Homo sapiens) genome, GRCh38/hg38 (Dec, 2013)
![]()

5. "design"をクリックします。
![]()

6. Resultsの表示を確認します。
![]()

7. ゲノムに対して特異的なターゲットを表示するために、"show highly specific target only"にチェックをいれて更新します（更新は自動で行われます）。
![]()

8. "20mer+PAM"が1で、なおかつ"12mer+PAM"と"8mer+PAM"の数がなるべく少ない標的を選択し、配列をコピーします。
![]()

9. SnapGene Viewerを開き、Edit -> Find -> Find DNA sequenceで配列検索スペースを開き、選択したプロトスペーサ配列"accaccaggctacgagcgga"を検索する
![]()
![]()

9. 緑色で表示されたプロトスペーサ配列"accaccaggctacgagcgga"とその3´末端に隣接するPAM結合サイト"cgg"にフィーチャーをつける。ストランドが把握しやすいように工夫する。
![]()
![]()
![]()

10. プロトスペーサ配列"accaccaggctacgagcgga"をもったガイドRNAを発現させるマテリアル（ベクター等）の作製に用いる一本鎖オリゴヌクレオチドを設計して注文する。

- （例）U6プロモータを介したガイドRNA発現ベクターを作製する場合
  1. U6プロモータを使ってガイドRNAを発現させる場合は、プロトスペーサ配列の5´末端がGでなければならない。
  2. また、[Addgene]（https://www.addgene.org/）に寄託されている[pX330-U6-Chimeric_BB-CBh-hSpCas9プラスミド]（https://www.addgene.org/42230/）などに対してBpiIによる制限酵素処理&ライゲーションでプロトスペーサ配列を組み込む場合には、BpiIに適合した突出末端を形成するようにアダプター配列をつけておく必要がある。
  - (i)(ii)を考慮した場合、プロトスペーサ配列"accaccaggctacgagcgga"をもったガイドRNAを発現させる[pX330-U6-Chimeric_BB-CBh-hSpCas9プラスミド]（https://www.addgene.org/42230/）を作製するには下記の二種類の一本鎖オリゴヌクレオチドが必要となる。
    - `5´-caccGaccaccaggctacgagcgga____-3´`
    - `3´-_____tggtggtccgatgctcgcctcaaa-5´`

11. 一本鎖オリゴヌクレオチドを注文します。
  - FASMACの場合：ウルトラオリゴ/逆相カラム精製/修飾なし
![Fig-2]()

12. 注文後、CRISPR-Cas9システムを動かすためのマテリアルの作製を行い、ゲノム編集実験を行う。詳しくは下記の参考文献を参照してください。
![Fig-2]()

##### 参考文献
  * 山本 卓、佐久間 哲史（2019）.「完全版 ゲノム編集実験スタンダード〜CRISPR-Cas9の設計・作製と各生物種でのプロトコールを徹底解説 (実験医学別冊)」 羊土社

##### 関連ツール
- [COSMID](https://crispr.bme.gatech.edu/)
  - 標的配列に対するオフターゲットサイトを予測するツール。ミスマッチ・ギャップの位置に基づいたスコアリング機能もついており、PCR等でオフターゲット解析をする場合の標的選定に活用できます。

- [Cas-OFFinder](http://www.rgenome.net/cas-offinder/)
  - 標的配列に対するオフターゲットサイトを予測するツール。ミスマッチやDNA側あるいはRNA側のギャップ（Bulge）を細かく指定できる。またCRISPRdirect同様に多くの生物種に対応している他、C57BL/6NJやFVB/NJといったマウス亜系統ゲノムでのオフターゲット検索もできます。

----

#### [CRISPROR](http://crispor.tefor.net)
- CRISPR-Cas9標的を検索できるウェブツール。標的検索だけでなく、そのオフターゲットの検索からプライマー設計までも含めた包括的な情報収集が可能。
    - [https://crispr.dbcls.jp](http://crispor.tefor.net)
    - [論文](https://doi.org/10.1093/nar/gky354)
    - [紹介動画 - 統合TV](https://doi.org/10.7875/togotv.2021.023)
    トップページ
    ![Fig-1]()      
    検索にヒットした標的候補のマップ（緑色が高い特異性をもつ標的）
    ![Fig-2]()
    検索にヒットした標的候補一覧表
    ![Fig-2]()
    "Cloning / PCR primers"をクリックするとガイドRNA構築に必要なオリゴヌクレオチド情報等が表示されます。
    ![Fig-2]()
    ![Fig-2]()
    ![fig-3]()
    "show all..."->"Off-target primers"をクリックすると、各オフターゲットサイトに対するPCRプライマーが表示されます。
    ![fig-4]()
- 標的候補一覧表の見方
  ![Fig-2]()
  - "Position/Strand"
    - 数字はターゲットの位置になります。
    - "fw/revでゲノムリファレンス上でどちらのstrand属するかを指します。
  - "Guide Sequence + PAM + Restriction Enzymes + Variants"
    - 標的の配列情報を指します。Restriction EnzymesはRFLP法で利用可能な制限酵素サイトを指します。VariantsはSNPを示しており、SNPを対象としたい場合はこの情報をもとに標的を選択することができます。
  - "MIT Specificity Score"
    - (Hsu et al. Nat Biotech 2013)に基づいた特異性スコアです。高いほど特異性が高いとされ、50以上が推奨されています。
  - "CFD Spec. score"
    - (Doench et al. Nat Biotech 2016)に基づいた特異性スコアです。
  - "Predicted Efficiency"
    - "Doench '16"は(Fusi et al. preprint 2015)[https://doi.org/10.1101/021568]と(Doench et al. Nat Biotech 2016)[https://doi.org/10.1038/nbt.3437]に基づいた予測切断活性のスコアです。CRISPR-Cas9をレンチウイルス導入したときの活性データを参考に作られています。
    - "Mor.-Mateos"は(Moreno-Mateos et al. Nat Method 2015)[https://doi.org/10.1038/nmeth.3543]に基づいた予測切断活性のスコアです。CRISPR-Cas9をレンチウイルス導入したときの活性データに基づいています。CRISPR-Cas9をゼブラフィッシュの胚にインジェクション導入したときの活性データを参考に作られています。in vivoでのゲノム編集を行う場合にはこちらのほうがより参考になると考えられています。
  - "Outcome"
    - "Out-of-Frame"は(Bae et al. Nat Method 2014)に基づいて欠失によるフレームシフトの起こりやすさを予測したものです。値をクリックすると実際の予測変異パターンを見ることができます。
    - "Lindel"は(Wei Chen et al, Nucleic Acids Research 2019)に基づいて欠失・挿入によるフレームシフトの起こりやすさを予測したものです。値をクリックすると実際の予測変異パターンを見ることができます。
  - "Off-targets for 0-1-2-3-4 mismatches + next to PAM"
    - オフターゲットサイトの数を標的配列とのミスマッチ数ごとに表示しています。最初の数字（ミスマッチ0でのオフターゲットサイト）が0である標的が最低限特異的な標的です。
  - "Genome Browser links to matches sorted by CFD off-target score"
    - CFD off-target scoreが高い順にオフターゲットサイトが表示されています。
    - マウスオーバーするとScoreとミスマッチ領域を参照できます。
    - クリックすると(UCSC Genome Browser)[http://genome.ucsc.edu/cgi-bin/hgTracks?db=hg19&lastVirtModeType=default&lastVirtModeExtraState=&virtModeType=default&virtMode=0&nonVirtPosition=&position=chr14%3A70883813%2D70883835&hgsid=1134497385_rBlE26ARXxLLm13wxuXQRiQjwHHc]にジャンプし、オフターゲットサイトの情報を細かく参照できます。

----

#### 【使用例】CRISPRORを使って、ノックアウトのための標的を設計する

1. 名前を入力します（入力しなくても可）。
MYOG
![Fig-2]()

2. 検索配列を入力します。
![Fig-2]()

3. 配列はSnapGene Viewerからドラッグ->コピーで取得します。今回は開始コドンから159bpを取得します。

入力配列：
atggagctgtatgagacatccccctacttctaccaggaaccccgcttctatgatggggaaaactacctgcctgtccacctccagggcttcgaaccaccaggctacgagcggacggagctcaccctgagccccgaggccccagggccccttgaggacaag
![Fig-2]()

4. 特異性を確認するゲノム+SNPデータベースを指定します。今回は最新のヒトゲノムリファレンスである"Homo sapiens- Human - UCSC Dec. 2013 (GRCh38/hg38) + SNPs: dbSNP148, Kaviar"とします。
ゲノム+SNPデータベース：Homo sapiens- Human - UCSC Dec. 2013 (GRCh38/hg38) + SNPs: dbSNP148, Kaviar
![Fig-2]()

5. PAM配列を指定します。今回は最も一般的なSpCas9の"NGG"とします。
PAM配列：NGG
![Fig-2]()

6. "SUBMIT"をクリックします。
![Fig-2]()

7. 結果が表示されるまで待ちます。
![Fig-2]()

8. 標的のリストが特異性が高い順に表示されます。ノックアウトする上では特異性が高く、なおかつ切断活性が低すぎなくて、フレームシフトが起こりやすい標的を選ぶのがベストです。今回の中では3番目にある"ACCACCAGGCTACGAGCGGA CGG"を選択します。
  1. 今回は次の基準で選んでみます。
  2. 特異性を示す"MIT Specificity Score"と"CFD Spec. score"がいずれも90を上回る
  3. 切断活性を示す"Doench '16"と"Mor.-Mateos"がいずれも25を下回らない
  4. フレームシフトの起こりやすさを示す"Out-of-Frame"と"Lindel"がいずれも60を上回る
  - これを満たすのは"ACCACCAGGCTACGAGCGGA CGG"、"TCGAACCACCAGGCTACGAG CGG"の二標的となります。どちらでもよいですが今回は"TCGAACCACCAGGCTACGAG CGG"を選んでみます。
![Fig-2]()

9. "Cloning / PCR primers"をクリックして、構築に必要なオリゴヌクレオチド情報を表示します。
![Fig-2]()

10. [pX330-U6-Chimeric_BB-CBh-hSpCas9プラスミド]（https://www.addgene.org/42230/）でガイドRNAを発現させたい場合は"U6 expression from an Addgene plasmid"の項目へ行き、"Select your Addgene plasmid:"で"pX330-U6-Chimeric_BB-CBh-hSpCas9(Zhang lab) + derivatives"を選択します。
![Fig-2]()

11. 配列が自動で更新されるので、更新された"Primers for gN20 guides"を記録します。
- gN20-guideRNA113fwU6sensepX330: CACCGaccaccaggctacgagcgga
- gN20-guideRNA113fwU6antisensepX330: AAACtccgctcgtagcctggtggtC
![Fig-2]()

12. 一本鎖オリゴヌクレオチドを注文します。
   - FASMACの場合：ウルトラオリゴ/逆相カラム精製/修飾なし

13. 注文後、CRISPR-Cas9システムを動かすためのマテリアルの作製を行い、ゲノム編集実験を行う。詳しくは下記の参考文献を参照してください。
![Fig-2]()

##### 参考文献
  * 山本 卓、佐久間 哲史（2019）.「完全版 ゲノム編集実験スタンダード〜CRISPR-Cas9の設計・作製と各生物種でのプロトコールを徹底解説 (実験医学別冊)」 羊土社

##### 関連ツール
- [CHOPCHOP](https://chopchop.cbu.uib.no)
  - Exonを参照しながらインタラクティブに標的を検索できるツール。
  - (統合TV)[https://doi.org/10.7875/togotv.2020.083]

### CRISPR-Cas9を使ったノックアウト結果の予測

#### DSBによる変異導入

  - CRISPR-Cas9やTALENといったゲノム編集ツールではDNA二本鎖切断（DSB）を引き起こし、その修復の結果発生するフレームシフト変異によってノックアウトを達成されます。
  - 教科書的にはこの時の変異導入は"ランダム"と説明されることも多いですが、実際にはある程度の傾向があることが知られています。
  - 哺乳類を問わず多くの生物種でみられるのが切断末端間にある相同配列がつながるような欠失変異パターンです。これらはMMEJやSSAなどといった修復経路によって引き起こされることが知られています。
  - またヒト等の培養細胞では切断面がC|Cとなっていると一塩基欠失によりCになったり、切断面でPAM側でないほうがTである場合はTTというようなリピート型の一塩基挿入が発生しやすかったりすることが知られています(文献)[https://dx.doi.org/10.1038%2Fnbt.4317]。
  - このような変異パターンを事前に予測するためのツールを紹介します。

#### [Microhomology-Predictor](http://www.rgenome.net/mich-calculator/)
- DSBによって引き起こされるMMEJ/SSAによる欠失変異パターンを予測するツール
    - [http://www.rgenome.net/mich-calculator/](http://www.rgenome.net/mich-calculator/)
    - [論文](http://dx.doi.org/10.1038/nmeth.3015)
    トップページ
    ![Fig-1]()      
    入力画面
    ![Fig-2]()
    検索結果
    ![fig-3]()
    詳細な変異パターン情報
    ![fig-4]()
    ![fig-5]()
- 結果画面の見方
  ![Fig-2]()
  - "Microhomology Score"
    - MMEJ/SSAによる欠失変異のトータルでの起こりやすさを表します。
  - "Out-of-frame Score"
    - MMEJ/SSAによる欠失変異の中でもフレームシフト変異となるパターンの起こりやすさを表します。
  - Microhomology：該当の変異パターンでつながる小さな相同配列（マイクロホモロジー配列）です。
  - Deletion Length：該当の変異パターンで引き起こされる欠失長を表します。
  - Pattern Score：該当の変異パターンの起こりやすさを表します。

----

#### 【使用例】Microhomology-Predictorを使って、ノックアウト結果を予測して標的を決定する

1. 今回はMYOG遺伝子の標的配列"ACCACCAGGCTACGAGCGGACGG"と"TCGAACCACCAGGCTACGAGCGG"を例にとって、どちらがノックアウトに相応しそうか調べてみます。

2. まず標的配列ごとに配列を入力します。Microhomology-Predictorは入力配列の中間に編集サイトがあるようにしなければちゃんと使えないのでそのようにします。
  1. 具体的な手順としては次のようになります。
  2. ゲノム情報をSnapGeneViewerを開き、標的配列を検索します。
  3. "Features"->"Add Cleavage Site..."で切断面を記録します。切断面はSpCas9の場合はPAM結合サイトの5´末端から-3ntの部分となります。
  4. 切断面から5´方向40bpに"Left_reference"というフィーチャーをつけます。
  5. 切断面から3´方向40bpに"Right_reference"というフィーチャーをつけます。
  6. "Left_reference"と"Right_reference"の部分の配列をまとめてコピーして入力します。

標的配列が"ACCACCAGGCTACGAGCGGACGG"である場合の入力配列：
atggagctgtatgagacatccccctacttctaccaggaaccccgcttctatgatggggaaaactacctgcctgtccacctccagggcttcgaaccaccaggctacgagcggacggagctcaccctgagccccgaggccccagggccccttgaggacaag


標的配列が"TCGAACCACCAGGCTACGAGCGG"である場合の入力配列：
atggagctgtatgagacatccccctacttctaccaggaaccccgcttctatgatggggaaaactacctgcctgtccacctccagggcttcgaaccaccaggctacgagcggacggagctcaccctgagccccgaggccccagggccccttgaggacaag

![Fig-2]()

3. Submitを押します。
![Fig-2]()

3. 結果が返ってきます。"Out-of-frame Score"を記録しておきましょう。

![Fig-2]()

4. それぞれの結果で"Out-of-frame Score"が高い方がフレームシフトを起こしやすいことが考えられるのでそちらを採用します。今回の場合はXXXです。
![Fig-2]()

#### [inDelphi](https://indelphi.giffordlab.mit.edu)
- DSBによって引き起こされるインデル変異パターンを予測するツール
    - [http://www.rgenome.net/mich-calculator/](http://www.rgenome.net/mich-calculator/)
    - [論文](https://doi.org/10.1038/s41586-018-0686-x)
    ページ画面
    ![Fig-1]()      
    入力画面
    ![Fig-2]()
    予測される変異パターンのアライメント
    ![fig-3]()
    予測される変異パターンのヒストグラム
    ![fig-4]()
    過去データとの比較（予測結果の評価）
    ![fig-5]()
    予測変異パターンの一覧
    ![fig-5]()
- "Comparison to predictions at 13,273,449 SpCas9 target sites in human exons and introns"の見方
  ![Fig-2]()
  - "Precision score"は変異の多様度予測したものとなります。この値が高いと細胞集団に対してゲノム編集した際に単一、もしくは少数の変異パターンに収束しやすいことを示します。もしこれが低いとモザイク度の高い編集となる可能性があります。
  - "Microhomology strength score"はマイクロホモロジー配列を介した変異が起こりやすいかどうかを示します。これが低い場合はNHEJ修復のようなマイクロホモロジー配列を介さないランダム性の高い変異が出現しやすくなると考えられます。
  - "Frameshift frequency"はインデルによるフレームシフトの起こりやすさを示します。

----

#### 【使用例】inDelphiを使って、ノックアウト結果を予測して標的を決定する

1. 今回はMYOG遺伝子の標的配列"ACCACCAGGCTACGAGCGGACGG"と"TCGAACCACCAGGCTACGAGCGG"を例にとって、どちらがノックアウトに相応しそうか調べてみます。

2. まず標的配列ごとに配列を入力します。inDelphiは切断面を境界として5´側、3´側配列を入力する必要があります。
  1. 具体的な手順としては次のようになります。
  2. ゲノム情報をSnapGeneViewerを開き、標的配列を検索します。
  3. "Features"->"Add Cleavage Site..."で切断面を記録します。切断面はSpCas9の場合はPAM結合サイトの5´末端から-3ntの部分となります。
  4. 切断面から5´方向40bpに"Left_reference"というフィーチャーをつけます。
  5. 切断面から3´方向40bpに"Right_reference"というフィーチャーをつけます。
  6. "Left_reference"と"Right_reference"の部分をそれぞれ左側と右側のフォームに入力します。

標的配列が"ACCACCAGGCTACGAGCGGACGG"である場合の入力配列：
atggagctgtatgagacatccccctacttctaccaggaaccccgcttctatgatggggaaaactacctgcctgtccacctccagggcttcgaaccaccaggctacgagcggacggagctcaccctgagccccgaggccccagggccccttgaggacaag


標的配列が"TCGAACCACCAGGCTACGAGCGG"である場合の入力配列：
atggagctgtatgagacatccccctacttctaccaggaaccccgcttctatgatggggaaaactacctgcctgtccacctccagggcttcgaaccaccaggctacgagcggacggagctcaccctgagccccgaggccccagggccccttgaggacaag

![Fig-2]()

2. PAM配列を指定します。今回は最も一般的なSpCas9の"NGG"とします。
PAM配列：NGG

3. "HCT116", "HEK293", "K562", "U2OS"の中でご自身が使われている細胞株をクリックします。
![Fig-2]()

3. 自動的に予測が始まるのでしばらく待ちます。
![Fig-2]()

3. 結果が返ってきます。"Frameshift frequency"を記録しておきましょう。

![Fig-2]()

4. それぞれの結果で"Frameshift frequency"が高い方がフレームシフトを起こしやすいことが考えられるのでそちらを採用します。今回の場合はXXXです。
![Fig-2]()

#### Microhomology-PredictorとinDelphiの使い分け
まずHEK293Tなどのヒト培養細胞においてはinDelphiの予測はかなり正確であることが示されています。
しかしながらinDelphiは機械学習ベースのツールであるため、学習対象にはなかった哺乳類以外の培養細胞、初代境内細胞、またin vivoでのゲノム編集ではその精度はかなり揺らぐのではないかと考えられます。
もちろん今後詳細な検証がなされていくかと思いますが、哺乳類以外の培養細胞、初代境内細胞、またin vivoでのゲノム編集では代わりにMicrohomology-Predictorのほうを活用してみてもよいかと思われます。
またMicrohomology-PredictorはTALENやZFNでも利用できるので、TALENやZFNを扱う場合にはMicrohomology-Predictorのほうを使用すべきです。

##### 関連ツール
- [SPROUT](https://zou-group.github.io/SPROUT)
  - primary human T cellsでのゲノム編集結果に基づいて作製された変異パターン予測ツール。primary human T cellsを扱う場合はこちらも参考になります。

----

## 2章. より応用的なゲノム編集のためのデータベース・ツールを知る

#### 応用的なゲノム編集について

ゲノム編集でできることはDSBによるノックアウトだけではありません。
ドナーを導入することで人工的な配列を挿入するノックインができますし、またDNAに対する脱アミノ酵素をニッカーぜ型Cas9に取り付けることで二本鎖切断を伴わない塩基置換（Base Editing）を実現できます。
特に最近では、ニッカーぜ型Cas9と融合させた逆転写酵素を利用して置換やインデルを加える方法（Prime Editing）が開発されています。
またこのようにCRISPR-Cas9、およびその派生技術が興隆する一方で、規制やライセンスの観点からZFNやTALENなども商業的に注目されています。
他にもゲノム編集から広がってRNA編集にもCRISPRが利用されつつあります。CRISPR-Cas13はその代表例で、RNAiよりも優れたノックダウン効果を示しています。
このように世界中でゲノム編集が使われるなかで、それらを解析する専用ツールやデータベースも開発されている状況です。
本章ではこのようなツールの一部を紹介し、ゲノム編集についてより理解を深めていただければと思います。

またこのようなツール・データベースに関しては演者が個人的にまとめていますので下記のQiitaのページをご参照いただければと思います。

##### ゲノム編集のためのデータベース・ツール一覧

(ゲノム編集系のバイオインフォマティクス)[https://qiita.com/KazukiNakamae/items/fa1c58351c1a8ce4c937]
(https://qiita.com/KazukiNakamae/items/fa1c58351c1a8ce4c937)[https://qiita.com/KazukiNakamae/items/fa1c58351c1a8ce4c937]

### CRISPR-Cas9によるノックイン設計ツール

ゲノム編集におけるノックインには非常にさまざまなものが知られています。
ドナーDNAを導入するタイプのノックインでは基本的に特定のDSB修復経路を利用しており、何を利用するかはどういったドナーDNAを扱うかによります。
たとえば相同組換え修復(HR)を利用する場合は500bp以上のホモロジーアームを両端に持たせる必要があります（Yao et al., 2017)[https://doi.org/10.1038/cr.2017.76]。
また、HDR/MMEJ/NHEJを利用する場合はドナーも直鎖化しておき、修復経路に応じた長さのホモロジーアームを持たせておく必要があります（HDR knock-in、HITI、SATI、PITCh）。
さらに一本鎖DNAをドナーとして利用する場合もあり、この場合はSSTRという経路が利用されます(2 hit 2 oligo, long donor)。

今回はMMEJ等を利用したノックイン（PITCh法）の設計ツールを紹介します。
MMEJ等を利用したノックインはホモロジーアームが20-40bpほどの相同配列（マイクロホモロジー）を取り付けるだけでドナーの作製ができるため、PCRによるアダプター付加のみでドナーを作製できます。
これは500bp以上の配列をゲノムから取得する必要があるHRなどと比べると、簡便でなおかつさまざまな生物種で利用可能であることが示されています（マウス、カエル、藻類？、ヒト、ハムスター、魚）。

#### PITCh designer 2.0
![Fig-2]()
入力例

### Base Editorによる塩基編集設計ツール

Base Editingに使う脱アミノ酵素をニッカーぜ型Cas9（Base Editor）には大きく分けて二つのタイプがあります。
シトシン（C）をチミン（T）に変換するシトシン型Base Editorとアデニン（A）をチミン（T）に変換するアデニン型Base Editorです。
これらはCas9が結合したゲノムの特定の範囲（Windowと呼びます）に対して作用し、上記の置換を行います。
WindowはBase Editorの種類によって違っており、以下のツールではそうしたWindowを考慮した上での標的配列設計を行うことができます。

#### BE-Designer
![Fig-2]()
入力例

### Base Editorによる塩基編集予測ツール

結合したゲノム箇所に塩基置換を導入できるBase Editorですが、Window内の目的とは異なる位置にC塩基またはA塩基がある場合はその塩基も同時に置換してしまうケースがあります。また場合によってはCからGへの変換などマイナーな塩基置換を発生させることもあり、100%指向的に置換変異を入れられるわけではありません。
そのため過去のBase Editingデータを学習し、置換パターンを事前に予測するツールも開発されています。これを使うことで変異の指向性をある程度予想することが可能です。

#### BE-Hive
![Fig-2]()
入力例

### Prime Editorによる小規模編集設計ツール

逆転写酵素を利用したゲノム編集手法であるPrime Editingはインデル置換が入り混じった複雑な小規模変異を導入可能ですが、そのために使うプロトスペーサー配列や逆転写テンプレート（RT Template：RTT）、プライマー結合サイト（Primer Binding Site：PBS）、そしてニック導入用のガイドRNA（nicking gRNA：ngRNA）など通常のCRISPR-Cas9による変異導入やBase Editorと比べると設計がやや複雑です。
以下のツールではそのような設計の複雑さを解消するために配列の自動設計機能を提供しています。

#### PrimeDesign
![Fig-2]()
入力例

### TALENによるノックアウト設計ツール

TALENはCRISPR-Cas9と同様に任意の配列に結合させてDNA二本鎖切断による変異導入することが可能なゲノム編集ツールです。
RNA-DNA結合のCRISPR-Cas9とは違い、タンパク質-DNA結合ですが、これをうまく設計するためのツールも開発されています。

#### TAL Effector Nucleotide Targeter 2.0
![Fig-2]()
入力例

### Cas13によるRNA編集設計ツール

CRISPR-Cas13はRNA対して配列特異的な結合をすることができます。
これによってRNAi以上の特異性でノックダウンを行えますが、その有効性は標的によってやや異なることが知られています。
このツールではそういった有効性を予測しつつ標的配列の選定を行うことが可能です。

#### Cas13design
![Fig-2]()
入力例

### ウイルスに対するゲノム編集設計データベース

昨今のコロナウイルスに代表されるように、RNAウイルスは科学者にとって大きな研究対象です。
CRISPR-Cas13を使ってターゲティングする際にはウイルスゲノムを参照する必要がありますが、このサイトでは標的とすることが可能な配列のデータベースを公開しています。

#### COMBAT crRNA Repository
![Fig-2]()
入力例

### サンガーシーケンスデータを使った変異分析ツール

一般的なサンガーシーケンスで読み出せる配列は一種類であり、細胞集団に対して一斉にゲノム編集を行ったサンプル（ポピュレーションサンプル）のジェノタイピングを行う場合はサブクローニングを行う必要があります。
しかし最近では、ゲノムPCR産物を直接サンガーシーケンサーによって解析する方法も開発されてきています。
TIDE解析はそうしたアプローチのもとでゲノム編集サンプルを解析する方法です。
通常の考え方では、ゲノムPCR産物を直接サンガーシーケンスで読み出した場合は様々な配列のシグナルが混ざり合って、塩基配列として読み出すことができません。しかしTIDE解析では、こうした混合シグナルをコンピュータ上で分離することで、ゲノム編集の結果で生じた配列パターンを明らかにすることが可能です。

#### TIDE
![Fig-2]()
入力例

### アンプリコンシーケンシングデータを使った変異分析ツール

ポピュレーションサンプルをアレルベースでのシーケンス解析するうえで最も高解像度な方法はアンプリコンシーケンスといえます。
しかしながらこうした解析は必ずしもゲノム編集に特化した形になっておらず、また解析にもそれなりの知識を要します。
そのためゲノム編集解析に特化したシーケンスデータ解析ツールが発表されています。
これらを使うことでゲノム編集という文脈のなかで理解しやすいデータを得ることが可能です。

#### CRISPResso2
![Fig-2]()
入力例

### UCSC genome browserでのCas9標的の確認

UCSCのgenomue browserではあらかじめCRISPR-Cas9標的のアノテーションが用意されています。
これを参照することで標的可能な部位をおおよそ見積もることが可能です。
また予測切断活性やオフターゲットも評価されており、このサイトだけでも十分な選定が可能となっています。

![Fig-2]()
入力例

### ガイドRNA先行研究データベース

CRISPR-Cas9が発表されて早9年が経とうとしており、これまでさまざまなゲノム標的でCRISPR-Cas9が利用されていきました。
こうした過去の実験データは徐々にデータベースとして収録されてきており、これを参考にポジコン標的等を選定することで効率的な実験デザインが可能となりそうです。

#### dbGuide

![Fig-2]()
入力例


### template-freeゲノム編集データベース

SNP配列の構築はノックインで実現されることが多いですが、MMEJを介した指向性のある変異導入を行えばドナーテンプレートを導入することなく、単純なノックアウトでSNP構築が可能です。
こうしたtemplate-freeな手法で構築可能なSNPはデータベース化されています。

#### MHcut Browser

![Fig-2]()
入力例

----

## 3章. ゲノム編集情報の安全な設計・解析・管理ツール

ゲノム編集を支援するデータベース・ツールは非常に多く発表されていますが、現状はほとんどのものは海外製であり、データ管理という観点で懸念が全くないわけではありません。
安全なゲノム編集設計・解析・管理を行うための国産ツールとして「GGGenome」および「Genome Editing Cloud」が開発されていますのでこちらを最後に紹介しておきます。

### GGGenome（+パッケージ版）によるオフターゲット検索

DBCLSが運営している商用利用可能な高速配列検索サイトです。
特定のゲノムを指定してミスマッチ・ギャップつきオフターゲットを検索することができます。
ある程度であれば検索長の制約はないので、一般的なCRISPR-Cas9のみならず様々なゲノム編集ツールでも利用ができます。

![Fig-2]()
入力例

またレトリバ社はGGGenomeのパッケージ版を販売しており、ローカルな環境で実行することができます。

![Fig-2]()
入力例

### Genome Editing Cloudの紹介

プラチナバイオ・凸版印刷が開発しているゲノム編集専用データ基盤です。
現在は商用利用可能なsgRNAの設計や活性予測、アンプリコンシーケンス解析機能を開発しており、解析データは凸版印刷のセキュアなクラウド内に保存することが可能です。
基本的に商業ベースのゲノム編集支援ツールを目指しており、要望に応じて機能拡充を行っていく予定です。
現在はクローズなテストを行っていますが、ご利用にご興味ある方は以下のアドレスまでご連絡ください。

![Fig-2]()
入力例

----

## 0章. 補遺

ゲノム編集をするうえで配列の情報収集は欠かせません。
補遺ではデモ資料で用意した配列情報を取得した流れを説明します。

### NCBI等から遺伝子の配列情報を取得する

1.	まずウェブ検索でアメリカ国立生物工学情報センター（NDBI）へアクセスする。
 
![Fig-2]()
入力例

2.	検索欄で「Gene」を選択して、「ATP5B」と入力して検索

![Fig-2]()
入力例

3.	検索対象をヒト（Homo sapiens）に限定するためにクリック
 
 ![Fig-2]()
 入力例

4.	遺伝子には複数の名前をもつものが存在する。ATP5Bの場合はATP5F1Bの「Aliases」欄に含まれていることから、ATP5B遺伝子はATP5F1B遺伝子と同一であることがわかる。したがって、このATP5F1Bをクリックして先に進む。

![Fig-2]()
入力例
 
5.	ATP5（ATP5F1B）遺伝子の総合情報が表示される。この中で今回は人のゲノム上の遺伝子配列が知りたいので「Genomic regions, transcripts, and products」の欄へ行って、GenBankをクリックする。

![Fig-2]()
入力例
 
6.	遺伝子配列に関する総合情報（GenBankフォーマット）が表示されるので、この情報をファイルとして保存するために「Send to」をクリック。
 
![Fig-2]()
入力例

7.	フォーマットとして「Comple Record」「File」「GenBank」を指定して、「Create File」でダウンロードする。そうすると「sequence.gb」というファイルが手にはいる。

![Fig-2]()
入力例
 
### SnapGeneViewerで配列情報をわかりやすく表示する

8.	gbファイル（GenBankファイル）を読み込むには専用のソフトが必要になる。今回はSnapGene Viewerという無料ソフトをダウンロードして使う。

![Fig-2]()
入力例
 
9.	SnapGene Viewerでsequence.gbを開くと次のようになる。小豆色の矢印がタンパク質に変換されるDNA配列となっている。今回はこの末端に人工的な配列を付加することを行うため、矢印先端のちょうど上の二重線をクリックして、「Sequence」タブで拡大表示する。

![Fig-2]()
入力例
 
10.	拡大すると以下のようになる。小豆色の線の上に表示されているのが該当するDNA二重鎖配列となっている。

![Fig-2]()
入力例

11. 単純なノックアウトする際には開始コドン付近を狙うが、特定のドメイン構造を破壊したい場合はアノテーションにしたがって標的とする箇所を見つけるとよい。またその情報がない場合は、文献情報やInterProといったツールを活用して機能性ドメインを探索することが考えられる。

![Fig-2]()
入力例

