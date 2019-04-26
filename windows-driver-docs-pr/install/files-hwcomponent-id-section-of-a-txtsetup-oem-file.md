---
title: TxtSetup.oem ファイルの Files.HwComponent.ID セクション
description: Files.HwComponent.ID セクションには、ユーザーが特定のコンポーネントのオプションを選択した場合にコピーするファイルが一覧表示します。 これらのセクションのいずれかの各 HwComponent セクションに記載の各オプションの存在である必要があります。
ms.assetid: a2c48a94-18a9-4efe-bdff-6c08bbbbabf9
keywords:
- Files.HwComponent.ID セクションの TxtSetup.oem ファイルのデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- Files.HwComponent.ID Section of a TxtSetup.oem File
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 92e6b773f0ae1377c51d76990863154c61b435ba
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341987"
---
# <a name="fileshwcomponentid-section-of-a-txtsetupoem-file"></a>TxtSetup.oem ファイルの Files.HwComponent.ID セクション


A**ファイル**。<em>HwComponent</em>**.**<em>ID</em>セクションには、ユーザーが特定のコンポーネントのオプションを選択した場合にコピーするファイルが一覧表示されます。 これらのセクションのいずれかに記載の各オプションの存在である必要があります*HwComponent*セクション。

``` syntax
[Files.HwComponent.ID]
filetype = diskN,filename[,DriverKey]
...
```

<a href="" id="files-hwcomponent-id"></a>**ファイル。** <em>HwComponent</em>**.**<em>ID</em>  
*HwComponent*の名前に対応する*HwComponent*ファイルのセクション。 *ID*に対応する*ID*エントリを*HwComponent*セクション。

<a href="" id="filetype"></a>*ファイルの種類*  
コピーするファイルの種類を識別します。 これらのエントリのいずれかがこれをコピーするには、各ファイルの存在*HwComponent*.*ID*します。

*Filetype*は次のシステム定義の値の 1 つです。

<a href="" id="driver"></a>**ドライバー**  
すべてのコンポーネントに対して有効です。 Windows では、ファイルをコピー %*systemroot %\\system32\\ドライバー。*

<a href="" id="dll"></a>**dll**  
すべてのコンポーネントに対して有効です。 ディスプレイ ドライバーの GDI 部分に便利です。 Windows では、ファイルをコピー %*systemroot %\\system32 します。*

<a href="" id="hal"></a>**hal**  
に対してのみ有効です、**コンピューター**コンポーネント。 Windows では、% にファイルをコピー*systemroot %\\system32\\hal.dll* x86 または *\\os\\winnt\\hal.dll*システム(x86) 以外のパーティション。

<a href="" id="inf"></a>**inf**  
すべてのコンポーネントに対して有効です。 デバイスの通常の INF ファイルを指定します。 このファイルは、フル インストール モードのセットアップ中、およびその他のデバイスのメンテナンス操作に使用されます。 ファイルのコピーを %*systemroot %\\system32*します。

<a href="" id="catalog"></a>**カタログ**  
ドライバーに対して有効です。 デバイスのカタログ ファイルを指定します。 任意のコンポーネントは必要ありません。 たとえば、**カタログ**= d1、 *mydriver.cat*します。 カタログのファイルの詳細については、WHQL のガイドラインを参照してください。

<a href="" id="detect"></a>**検出**  
有効な**コンピューター**コンポーネント (x86 のみ)。 指定すると、標準の x86 に置き換わりますハードウェア認識します。 Windows ファイルがコピー *c:\\ntdetect.com*します。

<a href="" id="diskn"></a>*diskN*  
ファイルをコピー元のディスクを識別します。 この値のエントリに一致する必要があります、**ディスク**セクション。

<a href="" id="filename"></a>*ファイル名*  
ディレクトリ パスまたはドライブを除く、ファイルの名前を指定します。 ファイルの完全名を形成するには、Windows が追加、 *filename*内のディスクの指定したディレクトリに、**ディスク**セクション。 ファイル名は 8 文字を超えないし、拡張機能は、次の 3 つの文字を超えない必要があります。

<a href="" id="driverkey"></a>*DriverKey*  
ファイルが型の場合は、このファイルのレジストリ サービス ツリー内に作成するキーの名前を指定します**ドライバー**します。 この値を使用してフォーム**Config** 。<em>DriverKey</em>セクション名。 この値は型のコンポーネントに必要な**scsi**します。

次の例は、**ファイル**。<em>HwComponent</em>**.**<em>ID</em>セクション、 *TxtSetup.oem*ファイル。

``` syntax
; ...
[Files.SCSI.oemscsi]
driver = d1,oemfs2.sys,OEMSCSI
inf = d1,oemsetup.inf
dll = d1, oemdrv.dll
catalog = d1, oemdrv.cat
; ...
```

 

 





