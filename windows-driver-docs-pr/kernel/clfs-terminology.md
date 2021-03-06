---
title: CLFS の関連用語
description: 次の一覧は、Common Log File System (CLFS) ドキュメントで使用される主な用語の定義を示しています。
Robots: noindex, nofollow
ms.assetid: d8511c5a-0181-4c54-acdc-e8a5892bb620
keywords:
- 一般的なログ ファイル システムの WDK カーネル、用語集
- CLFS WDK カーネル、用語集
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96c41d15b038d037c485dfa028a52736e57c66a1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343691"
---
# <a name="clfs-terminology"></a>CLFS の関連用語


次の一覧は、Common Log File System (CLFS) ドキュメントで使用される主な用語の定義を示しています。 これらの定義は、CLFS の会議中に適用されますが、それ以外の場合は適用されません可能性があります。 一般的な意味や意味これらの用語の多くがある定義をここに示すとは異なるその他のテクノロジのコンテキストでします。

<a href="" id="kernel-clfs-term-container"></a>**コンテナー**  
物理ディスクまたはその他の安定したストレージ メディア上の連続する範囲。 たとえば、コンテナーでは、連続したディスク ファイル可能性があります。

<a href="" id="kernel-clfs-term-sector"></a>**セクター**  
物理記憶域メディア上のアトミック I/O の単位。 セクターのサイズは、特定の記憶域デバイスのプロパティです。 たとえば、ハード ディスクには、512 バイトのセクター サイズがあります。

<a href="" id="kernel-clfs-term-log"></a>**ログ**  
基本ファイルと論理的に順序付けられたコンテナーのセット。 ベースのファイルは、ログのメタデータを保持し、コンテナーにログ レコードを保持します。 すべてのコンテナーは、同じサイズです。

<a href="" id="kernel-clfs-term-client"></a>**クライアント**  
アプリケーション、ドライバー、スレッド、または CLFS ログを使用するソフトウェアの他の単位。

<a href="" id="kernel-clfs-term-record"></a>**レコード**  
クライアントに追加したり、ログから読み取られたデータの単位。

<a href="" id="kernel-clfs-term-stream"></a>**ストリーム**  
ログ内のレコードの順序付きのサブセットです。 ログには、1 つまたは複数のストリームを持つことができます。 クライアントは、レコードと特定のストリームから読み取りレコードを追加します。 書き込まれた順序を決定する指定されたストリーム内のレコードを比較することができます。 異なるストリーム内のレコードを比較することはできません。 指定したストリームには、複数のクライアントを持つことができます。 たとえば、複数のスレッドでは、1 つのストリームにレコードを追加する可能性があります。 クライアントにストリームが表示されます、全体のログの場合と同様です。

<a href="" id="kernel-clfs-term-dedicated-log"></a>**専用ログ**  
ログを 1 つのみのストリームを持つことができます。

<a href="" id="kernel-clfs-term-multiplexed-log"></a>**ログを多重化**  
ログを複数のストリームを持つことができます。

<a href="" id="kernel-clfs-term-log-i-o-block"></a>**ログの I/O ブロック**  
CLFS は安定ストレージにアトミックに書き込まれるレコードのセットを収集しますバッファー。

<a href="" id="kernel-clfs-term-marshalling-area"></a>**マーシャ リング領域**  
一連のログの I/O ブロックを作成、維持、およびログ レコードを収集するため、CLFS クライアントによってスケジュールに安定ストレージに書き込むとします。 特定のマーシャ リング領域の揮発性メモリに割り当てられたログ I/O ブロックはすべて同じサイズです。

**注**  サイズで安定したストレージ (からそのマーシャ リング領域) に書き込まれるログの I/O ブロックが異なる場合でも、特定のマーシャ リング領域の (揮発性メモリ) 内ですべてのログ I/O ブロックが、同じサイズの場合。 たとえば、ログの I/O ブロックが強制された場合は完全な前に、安定ストレージに、安定ストレージにブロックの使用領域のみが書き込まれます。

 

<a href="" id="kernel-clfs-term-log-sequence-number--lsn"></a>**ログ シーケンス番号 (LSN)**  
指定したストリームにログ レコードを一意に識別する値を保持する非透過構造体。 クライアントでは、レコードを書き込むストリームを今後のレコードを識別するために使用できる LSN で取得バックアップします。 CLFS を割り当てるようにストリーム形式のレコードに増加するシーケンスが、Lsn。 つまり、ストリーム内のレコードに割り当てられている LSN は、以前同じストリームに書き込まれたレコードに割り当てられている LSN よりも大きいは常にします。

**注**  ストリームをまたぐレコードは比較されません。 つまり、どのレコードが最初に書き込まれたかを判断する、異なるストリームで 2 つのレコードの Lsn を比較することはできません。

 

<a href="" id="kernel-clfs-term-base-lsn"></a>**ベースの LSN**  
ストリームのクライアントがまだ必要なストリームで最も古いレコードの LSN。 クライアントは、ベースの LSN を更新します。

<a href="" id="kernel-clfs-term-last-lsn"></a>**最後の LSN**  
ストリームのクライアントがまだ必要なストリームの一番下のレコードの LSN。 通常、これは、ストリームに書き込まれた最も最近のレコードがクライアントにストリームのいくつか前のレコードを指す最後の LSN を手動で設定のオプションがあります。 最後の LSN を以前のレコードを手動で設定と呼びます*切り捨て*ストリーム。

<a href="" id="kernel-clfs-term-archive-tail"></a>**アーカイブ末尾**  
ログをアーカイブするための最も古いレコードの LSN が場所を作成していません。 すべてのログ アーカイブ末尾がされています。 アーカイブ末尾がないログと呼びます*短期*、され、アーカイブ末尾があるログが呼び出されます*短期間ではない*します。 クライアントは、ログが、アーカイブ末尾を指定する場合、クライアントはアーカイブ末尾の更新を担当します。

<a href="" id="kernel-clfs-term-active-portion-of-a-stream"></a>**ストリームのアクティブな部分**  
現在のクライアントによって使用されているストリームの部分。 アクティブな部分が指すベース LSN またはアーカイブ末尾レコードで始まる、小さい方です。 アクティブな部分は、最後の LSN を指すレコードで終わります。

 

 




