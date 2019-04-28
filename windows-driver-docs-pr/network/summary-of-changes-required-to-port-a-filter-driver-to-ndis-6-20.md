---
title: フィルター ドライバーを NDIS 6.20 に移植するために必要な変更の概要
description: フィルター ドライバーを NDIS 6.20 に移植するために必要な変更の概要
ms.assetid: faf83399-b9ac-41b3-a891-0142ded422b3
keywords:
- NDIS 6.20 WDK、フィルター ドライバーの移植
- 6.20 WDK の NDIS フィルター ドライバーの移植
- フィルター ドライバー WDK
- フィルター ドライバー WDK、NDIS 6.20 が動作への移植
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 333da3504df95acc12816b8e0b16396dd1bfe345
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366365"
---
# <a name="summary-of-changes-required-to-port-a-filter-driver-to-ndis-620"></a>フィルター ドライバーを NDIS 6.20 に移植するために必要な変更の概要





このトピックでは、NDIS 6 を移植するために必要な変更をまとめたものです。*x* NDIS 6.20 が動作するドライバーをフィルターします。

NDIS 6.20 が動作は、以前のバージョンの NDIS との下位互換性を保持します。 旧バージョンと互換性の詳細については、次を参照してください。 [NDIS 6.20 が動作の下位互換性](ndis-6-20-backward-compatibility.md)します。

NDIS 6.20 が動作環境をサポートするフィルター ドライバーを更新するには、ように、NDIS 6.x フィルター ドライバーを変更する必要があります。

<a href="" id="build-environment"></a>**環境を構築します。**  
NDIS620 NDIS61 または NDIS60 プリプロセッサの定義に置き換えます。

<a href="" id="general-porting-requirements"></a>**移植の一般的な要件**  
-   NDIS 6.20 バージョンでは、古い形式のインターフェイスを置き換えます。 古い形式のインターフェイスの詳細については、次を参照してください。 [NDIS 6.20 で古いインターフェイス](obsolete-interfaces-in-ndis-6-20.md)します。

-   64 を超えるプロセッサをサポートするために、次のインターフェイスを更新します。

    -   受信側 scaling (RSS)
    -   プロセッサ情報デバイス ドライバー インターフェイス
    -   リソース割り当て
    -   読み取り/書き込みロック

    64 を超えるプロセッサのサポートに関する詳細については、次を参照してください。 [NDIS 6.20 で 64 を超えるプロセッサのサポート](support-for-more-than-64-processors-in-ndis-6-20.md)します。

<a href="" id="driver-initialization"></a>**ドライバーの初期化**  
-   NDIS バージョンで 6.20 が動作を設定、 **MajorNdisVersion**と**MinorNdisVersion**のメンバー、 [ **NDIS\_フィルター\_ドライバー\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565515)に渡される構造体、 [ **NdisFRegisterFilterDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff562608)関数。

-   フィルター ドライバーのバージョンを設定、 **MajorDriverVersion**と**MinorDriverVersion**の NDIS メンバー\_フィルター\_ドライバー\_の特性構造適切なドライバー固有の値。

<a href="" id="filter-module-attach-and-detach-operations"></a>**フィルター モジュールのインポートし、操作のデタッチ**  
-   ミニポート アダプタの機能の提供情報インターフェイスの最新バージョンを使用します。 次のインターフェイスには、機能が更新されます。
    -   電源管理
    -   Receive side scaling (RSS)
    -   ハードウェア支援 (VMQ)
-   これらの構造の更新バージョンを使用します。

    -   [**NDIS\_フィルター\_アタッチ\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff565481)
    -   [**NDIS\_オフロード\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff566706)

    NDIS 構造のバージョン情報については、次を参照してください。 [NDIS バージョン情報を指定する](specifying-ndis-version-information.md)します。

<a href="" id="send-and-receive-data-paths"></a>**送信および受信データのパス**  
-   更新バージョンを使用して、 [ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)構造体。

-   必要に応じて、仮想マシン キュー (VMQ) インターフェイスをサポートします。 VMQ の詳細については、次を参照してください。 [NDIS 6.20 で仮想マシン キュー (VMQ)](virtual-machine-queue--vmq--in-ndis-6-20.md)します。

 

 





