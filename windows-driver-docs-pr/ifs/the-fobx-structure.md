---
title: FOBX 構造
description: FOBX 構造
ms.assetid: 95177b38-4ca5-49ed-9f9d-bafedd156044
keywords:
- 参照カウントの WDK RDBSS
- FOBX 構造体
- FILE_OBJECT 構造体
- WDK RDBSS の参照をカウント
- backpointers WDK RDBSS
- データ構造体の WDK ファイル システム
- RDBSS WDK ファイル システム、接続およびファイル構造
- リダイレクトされたサブシステムの WDK のバッファリングをドライブのファイル システム、接続およびファイル構造
- 接続が WDK RDBSS 構造体します。
- ファイル構造 WDK RDBSS
- WDK RDBSS 構造体
- WDK RDBSS の接続情報
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab55ede13f1e6ae15954af87adc9ae36156c61d4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344899"
---
# <a name="the-fobx-structure"></a>FOBX 構造


## <span id="ddk_the_fobx_structure_if"></span><span id="DDK_THE_FOBX_STRUCTURE_IF"></span>


ファイル オブジェクトの拡張機能 (FOBX) 構造体は RDBSS の拡張機能、 [**ファイル\_オブジェクト**](https://msdn.microsoft.com/library/windows/hardware/ff545834)構造体。 FOBX 構造体を指す、 **FileObjectExtension**フィールドに、ファイル オブジェクト。 FOBX 構造体には、次のものが含まれています。

-   署名と参照カウント

-   関連付けられている FCB 構造に戻りポインター

-   関連付けられている SRV 戻りポインター\_オープン構造体

-   このオープン構造に関するコンテキスト情報

-   ネットワークのミニ リダイレクターまたは FOBX 構造体の作成者によって要求された追加のストレージ

FOBX 構造体には、すべてのファイルのオブジェクトは、通常、I/O システムでは保存されませんごとに、必要な情報が含まれています。 ファイル オブジェクトに関する情報は、固定サイズのファイル システム オブジェクトで、I/O システムで格納されます。 FOBX 構造体は、ネットワークのミニ リダイレクターでファイルのオブジェクトに必要なその他の情報を処理します。

によって参照されている任意のファイル オブジェクト、構造体の FOBX、 **FsContext2**フィールドに、ファイル オブジェクト。 FOBX 構造体は、RDBSS 構造内の終端では通常、FOBX 構造体は現在もカウントされた参照にです。

FOBX フラグは、2 つのグループに分割されます。

-   ネットワークのミニ リダイレクターに表示されるフラグ

-   内部的に使用される RDBSS とネットワークのミニ リダイレクターを非表示フラグ

ネットワークのミニ リダイレクターに表示されるフラグは、考えられる FOBX フラグの下位 16 ビットで構成されます。 上位 16 ビットは、RDBSS によって内部的に使用するため予約されています。

 

 




