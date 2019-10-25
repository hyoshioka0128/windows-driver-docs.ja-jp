---
title: FOBX 構造
description: FOBX 構造
ms.assetid: 95177b38-4ca5-49ed-9f9d-bafedd156044
keywords:
- 参照カウント WDK RDBSS
- FOBX 構造体
- FILE_OBJECT 構造体
- カウント参照の WDK RDBSS
- backpointers WDK RDBSS
- データ構造の WDK ファイルシステム
- RDBSS WDK ファイルシステム、接続およびファイル構造
- リダイレクトされたドライブバッファリングサブシステム WDK ファイルシステム、接続とファイルの構造
- 接続構造 (WDK RDBSS)
- ファイル構造の WDK RDBSS
- 構造の WDK RDBSS
- 接続情報 WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30e8c203da55b0c8075f12fb5aa4cf56f9cca365
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840955"
---
# <a name="the-fobx-structure"></a>FOBX 構造


## <span id="ddk_the_fobx_structure_if"></span><span id="DDK_THE_FOBX_STRUCTURE_IF"></span>


ファイルオブジェクト拡張機能 (FOBX) 構造体は、[**ファイル\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_object)構造の RDBSS 拡張です。 FOBX 構造体は、ファイルオブジェクトの**Fileobjectextension**フィールドによってポイントされます。 FOBX 構造体には、次のものが含まれます。

-   署名と参照カウント

-   関連付けられた FCB 構造体への戻りポインター

-   関連付けられた SRV\_オープン構造体へのバックポインター

-   このオープン構造体に関するコンテキスト情報

-   ネットワークミニリダイレクターまたは FOBX 構造の作成者によって要求された追加のストレージ

FOBX 構造体には、ファイルオブジェクトごとに必要なすべての情報が含まれています。これは通常、i/o システムによって格納されるわけではありません。 ファイルオブジェクトに関する情報は、固定サイズのファイルシステムオブジェクトの i/o システムによって格納されます。 FOBX 構造体は、ネットワークミニリダイレクターによってファイルオブジェクトに必要なその他の情報を処理します。

File オブジェクトの FOBX 構造体は、file オブジェクトの**FsContext2**フィールドによって参照されます。 FOBX 構造体は、通常、RDBSS 構造体では無視されますが、FOBX 構造体は現在参照カウントされています。

FOBX フラグは、次の2つのグループに分割されます。

-   ネットワークミニリダイレクターに表示されるフラグ

-   RDBSS によって内部的に使用され、ネットワークミニリダイレクターからは見えないフラグ

ネットワークミニリダイレクターに表示されるフラグは、可能な FOBX フラグの下位16ビットで構成されます。 上位16ビットは、RDBSS によって内部で使用するために予約されています。

 

 




