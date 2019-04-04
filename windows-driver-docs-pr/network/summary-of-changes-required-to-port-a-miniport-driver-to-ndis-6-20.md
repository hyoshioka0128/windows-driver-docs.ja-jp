---
title: NDIS 6.20 が動作するためのミニポート ドライバーのポートへの変更の概要
description: ポートの NDIS 6.20 が動作するためのミニポート ドライバーに必要な変更の概要
ms.assetid: e52137ac-5333-4b62-8e26-686196d8ca78
keywords:
- NDIS 6.20 WDK、ミニポート ドライバーの移植
- ミニポート ドライバーには、NDIS 6.20 WDK の移植
- ミニポート ドライバー WDK
- ミニポート ドライバー WDK、NDIS 6.20 が動作への移植
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04461247d1e2de053a49944bee8437e27c2b413f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528703"
---
# <a name="summary-of-changes-required-to-port-a-miniport-driver-to-ndis-620"></a>ポートの NDIS 6.20 が動作するためのミニポート ドライバーに必要な変更の概要





このトピックでは、NDIS 6.20 が動作する NDIS 6.x ミニポート ドライバーを移植するために必要な変更をまとめたものです。

NDIS 6.20 が動作は、以前のバージョンの NDIS との下位互換性を保持します。 旧バージョンと互換性の詳細については、[NDIS 6.20 が動作の下位互換性](ndis-6-20-backward-compatibility.md)を参照してください。

NDIS 6.20 が動作環境をサポートするために、ミニポート ドライバーを更新するには、ように NDIS 6.x のミニポート ドライバーを変更する必要があります。

<a href="" id="build-environment"></a>**環境を構築します。**  
NDIS60 プリプロセッサの定義を置き換えます\_ミニポート\_ドライバーまたは NDIS61\_ミニポート\_NDIS620 ドライバー\_ミニポート\_ドライバー。

<a href="" id="general-porting-requirements"></a>**移植の一般的な要件**  
-   NDIS 6.20 バージョンでは、古い形式のインターフェイスを置き換えます。 古い形式のインターフェイスの詳細については、[NDIS 6.20 で古いインターフェイス](obsolete-interfaces-in-ndis-6-20.md)を参照してください。

-   64 を超えるプロセッサをサポートするために、次のインターフェイスを更新します。

    -   受信側 scaling (RSS)
    -   プロセッサ情報デバイス ドライバー インターフェイス
    -   リソースの割り当て
    -   読み取り/書き込みロック

    64 を超えるプロセッサのサポートに関する詳細については、[NDIS 6.20 で 64 を超えるプロセッサのサポート](support-for-more-than-64-processors-in-ndis-6-20.md)を参照してください。

<a href="" id="driver-initialization"></a>**ドライバーの初期化**  
-   NDIS バージョンで 6.20 が動作を設定、 **MajorNdisVersion**と**MinorNdisVersion**のメンバー、 [ **NDIS\_ミニポート\_ドライバー\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565958)に渡される構造体、 [ **NdisMRegisterMiniportDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff563654)関数。

-   ミニポート ドライバーのバージョンを設定、 **MajorDriverVersion**と**MinorDriverVersion**の NDIS メンバー\_ミニポート\_ドライバー\_特性適切なドライバー固有の値構造体。

-   NDIS の直接の OID 要求エントリ ポイントを定義\_ミニポート\_ドライバー\_特性構造体。 直接の OID 要求インターフェイスのサポートが NDIS 6.1 ドライバーでは省略可能が、ドライバーの NDIS 6.20 が動作するために必須です。 ミニポート ドライバー直接 OID 要求インターフェイスの詳細については、[ミニポート アダプター OID 要求](miniport-adapter-oid-requests.md)を参照してください。

<a href="" id="miniport-adapter-initialization"></a>**ミニポート アダプタの初期化**  
-   ミニポート アダプタの機能の提供情報インターフェイスの最新バージョンを使用します。 次のインターフェイスには、機能が更新されます。
    -   電源管理
    -   受信側 scaling (RSS)
    -   ハードウェア支援 (VMQ)
-   これらの構造の更新バージョンを使用します。

    -   [**NDIS\_ミニポート\_アダプター\_全般\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)
    -   [**NDIS\_再起動\_全般\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff567260)
    -   [**NDIS\_受信\_スケール\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff567228)
    -   [**NDIS\_ミニポート\_アダプター\_ハードウェア\_支援\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)

    NDIS 構造のバージョン情報については、[NDIS バージョン情報を指定する](specifying-ndis-version-information.md)を参照してください。

<a href="" id="send-and-receive-code-paths"></a>**コード パスの送受信**  
-   NDIS 6.20 ドライバーは、受信側をサポートする必要があります (RST) をスロットル処理では割り込みを受信します。 *ReceiveThrottleParameters*のパラメーター、 [ *MiniportInterruptDPC* ](https://msdn.microsoft.com/library/windows/hardware/ff559398)と[ *MiniportMessageInterruptDPC* ](https://msdn.microsoft.com/library/windows/hardware/ff559411) DPC ハンドラー関数を指す、 [ **NDIS\_受信\_スロットル\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567241)構造体。 エントリを遅延プロシージャ呼び出し (DPC) ハンドラー、 **MaxNblsToIndicate** NDIS のメンバー\_受信\_スロットル\_の最大数を指定するパラメーター構造体[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)ミニポート ドライバーを指定する必要があります、DPC 構造。 RST の詳細については、[受信側スロットル NDIS 6.20](receive-side-throttle-in-ndis-6-20.md)を参照してください。

-   更新バージョンを使用して、 [ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)構造体。

-   必要に応じて、仮想マシン キュー (VMQ) インターフェイスをサポートします。 VMQ の詳細については、[NDIS 6.20 で仮想マシン キュー (VMQ)](virtual-machine-queue--vmq--in-ndis-6-20.md)を参照してください。

 

 





