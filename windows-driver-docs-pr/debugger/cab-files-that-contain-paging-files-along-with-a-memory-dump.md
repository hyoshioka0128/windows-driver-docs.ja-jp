---
title: ページ ファイルと共にメモリ ダンプを含む CAB ファイル
description: ページング ファイルと共にキャビネット (CAB) ファイルでは、メモリ ダンプ ファイルを配置できます。
ms.assetid: 89B54522-1B21-4E4E-9AF3-1F637E3BA50F
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a16260eaa2a95de7a60d7374f7ecba009376aaf1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373954"
---
# <a name="cab-files-that-contain-paging-files-along-with-a-memory-dump"></a>ページ ファイルと共にメモリ ダンプを含む CAB ファイル


ページング ファイルと共にキャビネット (CAB) ファイルでは、メモリ ダンプ ファイルを配置できます。 Windows デバッガーでは、メモリ ダンプ ファイルを分析、したときにダンプ ファイルの作成時にページ アウトされたメモリを含む、完全なビューのメモリを提示するのにページング ファイルを使用できます。

たとえば、MyCab.cab をという名前の CAB ファイルには、これらのファイルが含まれています。

Memory.dmp Cabmanifest.xml Pagefile.sys Cabmanifest.xml 次のようとします。

```XML
<?xml version="1.0" encoding="UTF-8"?>
<WatsonPageFileManifest>
  <Pagefiles>
    <Pagefile Name="pagefile.sys"></Pagefile>
  </Pagefiles>
</WatsonPageFileManifest>
```

これらのコマンドを入力して、CAB ファイルを開くことができます。

-   **windbg /z MyCab.cab**
-   **kd /z MyCab.cab**

デバッガーは、デバッグ セッションに含まれる、ページング ファイルの一覧については、Cabmanifest.xml を読み取ります。 この例では、1 つだけのページング ファイルです。 デバッガーでは、ページング ファイルをデバッグ セッション中に使用可能なターゲット情報ファイル (TIF) ファイルに変換します。 デバッガーは、TIF へのアクセスがあるため、ダンプ ファイルの作成時にページ アウトされたメモリを表示できます。

ページング ファイルの数は、CAB ファイルに関係なく、デバッガーは Cabmanifest.xml に記載されているページング ファイルのみを使用します。 3 つのページング ファイルを一覧表示する CAB のマニフェスト ファイルの例を次に示します。

```XML
<?xml version="1.0" encoding="UTF-8"?>
<WatsonPageFileManifest>
  <Pagefiles>
    <Pagefile Name="pagefile1.sys"></Pagefile>
    <Pagefile Name="pagefile2.sys"></Pagefile>
    <Pagefile Name="swapfile.sys"></Pagefile>
  </Pagefiles>
</WatsonPageFileManifest>
```

Cabmanifest.xml、ページング ファイルは、Windows がそれらを使用する同じ順序で表示する必要があります。 これは、レジストリ内で出現する順序で表示されている必要があります。

CAB ファイルに格納されているメモリ ダンプ ファイルには、完全メモリ ダンプをする必要があります。 コントロール パネルを使用して、クラッシュが発生したときに、完全メモリ ダンプを作成する Windows を構成することができます。 たとえば、Windows 8 に進んで**コントロール パネルの &gt;システムとセキュリティ&gt;システム&gt;システムの詳細設定&gt;起動と回復**します。 コントロール パネルを使用する代わりに、このレジストリ エントリの値を 1 に設定できます。

**HKLM**\\**SYSTEM**\\**CurrentControlSet**\\**Control**\\**CrashControl**\\**CrashDumpEnabled**

Windows 8.1 以降、Windows を再起動すると、ページング ファイルの内容を保持するために Windows を構成できます。

ページング ファイルを Windows の再起動時に保存することを指定するには、このレジストリ エントリの値を 1 に設定します。

**HKLM**\\**SYSTEM**\\**CurrentControlSet**\\**Control**\\**CrashControl**\\**SavePageFileContents**

 

 





