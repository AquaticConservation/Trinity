# Trinity
RNA-Seq De novo

## トランスクリプトームの定義

トランスクリプトーム（transcriptome）は、広義には特定の生理条件下で細胞内に存在する全ての転写産物の集合を指し、メッセンジャーRNA（mRNA）、リボソームRNA（rRNA）、転移RNA（tRNA）、非コードRNA（ncRNA）を含む。狭義には全てのmRNAの集合を指す。

RNA-Seq（RNAシーケンシング）は、次世代シーケンシング技術を用いた最新のトランスクリプトーム解析技術である。この技術により、特定の細胞または組織の状態下でほぼ全ての転写産物の配列情報と発現情報が包括的かつ迅速に取得できる。これには、タンパク質をコードするmRNAや様々な非コードRNA、遺伝子選択的スプライシングによる異なる転写産物の発現量が含まれる。転写産物の構造と発現レベルの解析に加えて、未知の転写産物や希少な転写産物も発見されるため、遺伝子発現の差異、遺伝子構造の変異、分子マーカーのスクリーニングなど生命科学の重要な問題を正確に解析できる。

## アセンブリソフトウェアと使用法

### リードの前処理手順

1. Rcorrectorを使用してランダムな配列エラーを修正する。
2. 修正できないリードを削除する。
3. Fastpを使用してシーケンシングアダプターと低品質な配列を除去する。
4. Bowtie2を使用して細胞小器官のリード（cpDNA、mtDNA、または両方）をフィルタリングする。この操作により、細胞小器官のリードのみを含むファイルが生成され、Fast-Plastを用いたプラスチドのアセンブリに利用できる。**サンゴの場合+藻類?**
5. FastQCを実行してリードの品質をチェックし、over-represented readsを検出する。
6. 過剰に表現されているリードを削除する。

## Singularity を使用した Trinity の実行
Singularity は Docker よりも簡単かつ安全に使用でき、Trinity を実行するための推奨方法である。 Trinity のすべての最新リリースには、Trinity Singularity イメージアーカイブからダウンロードできる [Singularity イメージ (.simg)](https://data.broadinstitute.org/Trinity/TRINITY_SINGULARITY/) が含まれています。 Singularity がインストールされており、.simg ファイルがダウンロードされている場合は、次のように Trinity を実行できます。

```
    %  singularity exec -e Trinity.simg  Trinity \
          --seqType fq \
          --left `pwd`/reads_1.fq.gz  \
          --right `pwd`/reads_2.fq.gz \
          --max_memory 1G --CPU 4 \
          --output `pwd`/trinity_out_dir
```
