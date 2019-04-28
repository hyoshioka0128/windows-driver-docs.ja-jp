---
title: NDIS 6.20 が動作するためのプロトコル ドライバーに移植する変更の概要
description: プロトコル ドライバーを NDIS 6.20 に移植するために必要な変更の概要
ms.assetid: d47b29a5-3385-4023-b94c-5cfbc225f48a
keywords:
- NDIS 6.20 WDK、プロトコルのドライバーの移植
- NDIS 6.20 WDK にプロトコル ドライバーの移植
- プロトコル ドライバー WDK
- プロトコル ドライバー WDK、NDIS 6.20 が動作への移植
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: deed1d77b98591e6be28971a09e706d601647c9b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366354"
---
# <a name="summary-of-changes-required-to-port-a-protocol-driver-to-ndis-620"></a>プロトコル ドライバーを NDIS 6.20 に移植するために必要な変更の概要





このトピックでは、NDIS 6 を移植するために必要な変更をまとめたものです。*x*プロトコル ドライバーに NDIS 6.20 が動作します。

NDIS 6.20 が動作は、以前のバージョンの NDIS との下位互換性を保持します。 旧バージョンと互換性の詳細については、次を参照してください。 [NDIS 6.20 が動作の下位互換性](ndis-6-20-backward-compatibility.md)します。

NDIS 6.20 が動作環境をサポートするためにプロトコル ドライバーを更新するには、ように NDIS 6.x プロトコルのドライバーを変更する必要があります。

<a href="" id="build-environment-------"></a>**環境を構築します。**   
NDIS620 NDIS61 または NDIS60 プリプロセッサの定義に置き換えます。

<a href="" id="general-porting-requirements-------"></a>**移植の一般的な要件**   
-   NDIS 6.20 バージョンでは、古い形式のインターフェイスを置き換えます。 古い形式のインターフェイスの詳細については、次を参照してください。 [NDIS 6.20 で古いインターフェイス](obsolete-interfaces-in-ndis-6-20.md)します。

-   64 を超えるプロセッサをサポートするために、次のインターフェイスを更新します。

    -   受信側 scaling (RSS)
    -   プロセッサ情報デバイス ドライバー インターフェイス
    -   リソース割り当て
    -   読み取り/書き込みロック

    64 を超えるプロセッサのサポートに関する詳細については、次を参照してください。 [NDIS 6.20 で 64 を超えるプロセッサのサポート](support-for-more-than-64-processors-in-ndis-6-20.md)します。

<a href="" id="driver-initialization-------"></a>**ドライバーの初期化**   
-   NDIS バージョンで 6.20 が動作を設定、 **MajorNdisVersion**と**MinorNdisVersion**のメンバー、 [ **NDIS\_プロトコル\_ドライバー\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff566825)に渡される構造体、 [ **NdisRegisterProtocolDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff564520)関数。

-   プロトコル ドライバーのバージョンを設定、 **MajorDriverVersion**と**MinorDriverVersion**の NDIS メンバー\_プロトコル\_ドライバー\_特性適切なドライバー固有の値構造体。

<a href="" id="protocol-bind-and-unbind-operations-------"></a>**プロトコルのバインドし、操作をバインド解除**   
-   ミニポート アダプタの機能の提供情報インターフェイスの最新バージョンを使用します。 次のインターフェイスには、機能が更新されます。
    -   電源管理
    -   電源管理
    -   受信側 scaling (RSS)
    -   ハードウェア支援 (VMQ)
-   これらの構造の更新バージョンを使用します。

    -   [**NDIS\_バインド\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff564832)
    -   [**NDIS\_オフロード\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff566706)

    NDIS 構造のバージョン情報については、次を参照してください。 [NDIS バージョン情報を指定する](specifying-ndis-version-information.md)します。

<a href="" id="send-and-receive-data-paths-------"></a>**送信および受信データのパス**   
-   更新バージョンを使用して、 [ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)構造体。

-   必要に応じて、仮想マシン キュー (VMQ) インターフェイスをサポートします。 VMQ の詳細については、次を参照してください。 [NDIS 6.20 で仮想マシン キュー (VMQ)](virtual-machine-queue--vmq--in-ndis-6-20.md)します。

 

 





