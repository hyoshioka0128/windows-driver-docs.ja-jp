---
title: いる CoNDIS TAPI の初期化
description: いる CoNDIS TAPI の初期化
ms.assetid: eabb2038-ab64-4f48-8c94-e47d1139727b
keywords:
- いる CoNDIS WAN ドライバー WDK ネットワーク、TAPI サービス
- 電話サービス initiliazing WDK WAN
- ネットワーク、初期化中にいる CoNDIS TAPI WDK
- いる CoNDIS TAPI の初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5fe9e7a297bb7c48b293bf69cf777a3e636b5ed6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549205"
---
# <a name="condis-tapi-initialization"></a>いる CoNDIS TAPI の初期化





このセクションでは、いる CoNDIS WAN ミニポート ドライバーがアプリケーションの場合は、その TAPI 機能を列挙する方法について説明します。 これらの TAPI 機能が構成されます。

-   ミニポート ドライバーでは--の回線デバイスには、回線デバイス、モデム、fax ボード、および ISDN カードの数。

-   情報 - 特定の行の行情報が含まれます、たとえば、行識別子と、行を音声およびデータの同時転送のサポート チャネルのアドレス (電話番号) の数。

-   デバイスの行に対する特定のチャネルのアドレス情報アドレス情報が含まれます、たとえば、呼び出し元 (呼び出し元の ID) とアクティブな呼び出し可能な数の id には。

基になるハードウェアに関する情報を取得するには、NDPROXY は行とチャネル アドレスの機能の要求を発行します。 つまり、NDPROXY ドライバーはいる CoNDIS WAN ミニポート ドライバーの TAPI 機能を照会します。 NDPROXY ドライバーの呼び出し、 [ **NdisCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561711)ミニポート ドライバーの TAPI 機能のクエリを実行する関数。 この呼び出しで NDPROXY 渡します、NDIS\_OID\_要求の構造。 NDPROXY NDIS で、次を指定する\_OID\_要求。

-   **NdisRequestQueryInformation**値、 **RequestType**メンバー

-   ミニポート ドライバーから取得する TAPI 機能を指定するオブジェクト識別子 (OID)、 **Oid**メンバー

-   返される TAPI 機能情報を保持するバッファー、 **InformationBuffer**メンバー

NDPROXY ドライバーによっている CoNDIS WAN ミニポート ドライバーに送信されるすべてのクエリは、同期または非同期で完了できます。 いる CoNDIS WAN ミニポート ドライバーでは、そのクエリをすぐに完了できない NDIS を単に返すことを決定します場合\_状態\_PENDING と呼び出し、 [ **NdisMCmOidRequestComplete** 。](https://msdn.microsoft.com/library/windows/hardware/ff563551)関数内からその*ProtocolCoOidRequest*クエリが完了したことに機能します。

後いる CoNDIS WAN ミニポート ドライバーがで指定されている新しいアドレス ファミリの登録に関する NDPROXY を通知[いる CoNDIS TAPI 登録](condis-tapi-registration.md)、NDPROXY クエリの TAPI に固有の機能を決定する次の Oid、いる CoNDIS WAN ミニポート ドライバーと、ミニポート ドライバーの NIC

-   NDPROXY クエリ ミニポート ドライバー [OID\_CO\_TAPI\_CM\_CAP](https://msdn.microsoft.com/library/windows/hardware/ff569096)ミニポート ドライバーのデバイスでサポートされている行の数を決定する (デバイスをTAPI サービスを提供)。 この OID には、次の行に複数の異なる行の機能があるかどうかを示すミニポート ドライバーも要求します。

-   NDPROXY は次のミニポート ドライバーに問い合わせて[OID\_CO\_TAPI\_行\_CAP](https://msdn.microsoft.com/library/windows/hardware/ff569098)指定した行のテレフォニー機能を判断します。 この OID には、この行のアドレスがアドレスの種類の異なる機能を持つかどうかを示すにミニポート ドライバーも要求します。
    -   場合、前のクエリの OID\_CO\_TAPI\_CM\_ミニポート ドライバーのデバイスの 1 行のみをサポートしていること、または NDPROXY がデバイスでは、複数の行を行と同じ機能をサポートする場合、CAP が示されますOID のクエリに\_CO\_TAPI\_行\_デバイスの行の機能を取得する 1 回だけに大文字です。 この場合、ミニポート ドライバーによって返される行の機能は、デバイス上のすべての行に適用されます。
    -   NDPROXY OID をクエリする必要があります、デバイスは、複数の異なる行の機能を備えた複数の行をサポートする場合\_CO\_TAPI\_行\_各行の行の機能を取得する行ごとに 1 回の上限。
-   NDPROXY が最後に、ミニポート ドライバーをクエリ[OID\_CO\_TAPI\_アドレス\_CAP](https://msdn.microsoft.com/library/windows/hardware/ff569095)指定行に指定されたアドレスのテレフォニー機能を判断します。
    -   場合 OID の前のクエリ\_CO\_TAPI\_行\_CAP 行が 1 つのアドレスをサポートしているまたは行のすべてのアドレスに、アドレスと同じ機能があることを示しました NDPROXY クエリ OID\_CO\_TAPI\_アドレス\_行上のすべてのアドレスの機能を決定する上限を 1 回だけです。
    -   NDPROXY に OID が照会行では、複数の異なる機能を備えた複数のアドレスをサポートする場合\_CO\_TAPI\_アドレス\_行の各アドレスに対して 1 回の上限。

NDPROXY ドライバーでは、TAPI 列挙 Oid を使用して取得情報を使用して、次の操作を行います。

-   TAPI の後続の呼び出しの TAPI パラメーターを作成します。

-   承認または後続の受信 TAPI 呼び出しを拒否するかどうかを決定します。

-   後続の受信 TAPI 呼び出しを受信するには、1 つまたは複数 TAPI サービス アクセス ポイント (Sap) を登録します。

 

 





