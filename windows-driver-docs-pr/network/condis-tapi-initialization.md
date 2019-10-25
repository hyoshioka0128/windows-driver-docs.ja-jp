---
title: CoNDIS TAPI の初期化
description: CoNDIS TAPI の初期化
ms.assetid: eabb2038-ab64-4f48-8c94-e47d1139727b
keywords:
- CoNDIS WAN ドライバー WDK ネットワーク、TAPI サービス
- 電話 services WDK WAN、initiliazing
- 接続 TAPI WDK ネットワーク, 初期化
- CoNDIS TAPI を初期化しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78c21c9f178d70dbe353afc8034b5c4e08910baf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835053"
---
# <a name="condis-tapi-initialization"></a>CoNDIS TAPI の初期化





このセクションでは、CoNDIS WAN ミニポートドライバーがアプリケーションの TAPI 機能を列挙する方法について説明します。 これらの TAPI 機能は次のもので構成されます。

-   ミニポートドライバーがサポートするラインデバイスの数。たとえば、モデム、fax ボード、ISDN カードなどがあります。

-   特定の行に関する情報--行情報には、回線識別子や、回線が音声とデータを同時に送信するためにサポートするチャネルアドレス (電話番号) の数などが含まれます。

-   デバイス上の特定のチャネルアドレスに関する情報--アドレス情報には、たとえば、呼び出し元 (呼び出し元 ID) の id や可能なアクティブな呼び出しの数などが含まれます。

基になるハードウェアに関する情報を取得するために、NDPROXY は回線およびチャネルアドレスの機能に関する要求を発行します。 つまり、NDPROXY ドライバーは、CoNDIS WAN ミニポートドライバーの TAPI 機能に対してクエリを行います。 NDPROXY ドライバーは、ミニポートドライバーの TAPI 機能を照会する[**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)関数を呼び出します。 この呼び出しでは、NDPROXY は、NDIS\_OID\_要求構造を渡します。 NDPROXY は、NDIS\_OID\_要求で次を指定します。

-   **RequestType**メンバーの**NdisRequestQueryInformation**値

-   **Oid**メンバーのミニポートドライバーから取得する TAPI 機能を指定するオブジェクト識別子 (oid)

-   **Informationbuffer**メンバーで返される TAPI 機能情報を保持するバッファー

NDPROXY ドライバーによって CoNDIS WAN ミニポートドライバーに送信されるすべてのクエリは、同期的または非同期的に完了できます。 CoNDIS WAN ミニポートドライバーがクエリをすぐに完了できないと判断した場合は、単に NDIS\_\_STATUS を返し、その内から[**NdisMCmOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmoidrequestcomplete)関数を呼び出すことができます。クエリが完了したときに機能します。

Condis WAN ミニポートドライバーが、 [condis tapi の登録](condis-tapi-registration.md)で指定されている新しいアドレスファミリの登録について ndproxy に通知した後、ndproxy は次の oid を照会して、condis wan ミニポートドライバーの TAPI 固有の機能を決定します。およびミニポートドライバーの NIC です。

-   NDPROXY は、ミニポートドライバーに[OID\_CO\_tapi\_CM\_cap](https://docs.microsoft.com/windows-hardware/drivers/network/oid-co-tapi-cm-caps)を照会して、ミニポートドライバーのデバイス (tapi サービスを提供するデバイス) でサポートされる行の数を決定します。 また、この OID は、これらの行の線の機能が異なるかどうかを示すためにミニポートドライバーに要求します。

-   NDPROXY next は、ミニポートドライバーに[OID\_CO\_TAPI\_ライン\_cap](https://docs.microsoft.com/windows-hardware/drivers/network/oid-co-tapi-line-caps)を照会し、指定された回線のテレフォニー機能を決定します。 また、この OID は、この行のアドレスが異なるアドレス機能を持つかどうかを示すためにミニポートドライバーに要求します。
    -   前に示した OID\_CO\_TAPI\_CM\_CAP で、ミニポートドライバーのデバイスが1つの行しかサポートしていないことが示された場合、またはデバイスが同じ回線機能を持つ複数の行をサポートしている場合は、NDPROXY は OID を照会する必要があり\_デバイスの回線機能を取得するには、\_TAPI\_ライン\_キャップを1回だけ実行します。 この場合、ミニポートドライバーによって返される回線機能は、デバイス上のすべての行に適用されます。
    -   デバイスで回線機能が異なる複数の行がサポートされている場合、NDPROXY では、各行の行の機能を取得するために、1行につき1回、\_TAPI\_\_ラインを使用して\_OID を照会する必要があります。
-   最後に、NDPROXY は、ミニポートドライバーに[OID\_CO\_TAPI\_アドレス\_cap](https://docs.microsoft.com/windows-hardware/drivers/network/oid-co-tapi-address-caps)を照会して、指定された行の指定されたアドレスのテレフォニー機能を特定します。
    -   OID\_CO\_TAPI\_LINE\_CAP の前のクエリで、回線が1つのアドレスのみをサポートしていること、または回線上のすべてのアドレスが同じアドレス機能を持つことが示された場合、NDPROXY は OID\_CO\_TAPI @no__t_ を照会し6_ アドレス\_キャップは、その行のすべてのアドレスの機能を決定するために1回だけです。
    -   1つの回線が異なる機能を持つ複数のアドレスをサポートしている場合、NDPROXY は OID を照会して、回線上の各アドレスに対して1回ずつ、\_TAPI\_\_アドレスを\_します。

NDPROXY ドライバーは、次の操作を行うために、TAPI 列挙 Oid で取得した情報を使用します。

-   以降の TAPI 呼び出し用に TAPI パラメーターを作成します。

-   後続の受信 TAPI 呼び出しを受け入れるか拒否するかを決定します。

-   後続の受信 TAPI 呼び出しを受信する1つ以上の TAPI サービスアクセスポイント (Sap) を登録します。

 

 





