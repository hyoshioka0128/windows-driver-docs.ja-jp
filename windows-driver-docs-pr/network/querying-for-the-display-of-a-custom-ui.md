---
title: カスタム UI の表示のクエリ
description: カスタム UI の表示のクエリ
ms.assetid: 89f39281-db97-4cbe-8753-43ab30d840c8
keywords:
- カスタム UI WDK ネイティブ 802.11 IHV UI 拡張 DLL、クエリ
- カスタム UI 表示のクエリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88a378faf4569b5a49fb76c9603522632c0eaf86
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844891"
---
# <a name="querying-for-the-display-of-a-custom-ui"></a>カスタム UI の表示のクエリ




 

オペレーティングシステムは、ネイティブ 802.11 IHV Extensions DLL に対してクエリを実行し、DLL に表示するカスタム UI があるかどうかを判断できます。 ワイヤレス LAN (WLAN) アダプターが WLAN ネットワーク接続プロセス内の次のいずれかのフェーズに切り替わるたびに、オペレーティングシステムは DLL に対してクエリを実行します。

<a href="" id="pre-association-------"></a>**事前関連付け**   
IHV 拡張 DLL が事前関連付け操作を開始する前の接続フェーズ。 事前関連付け操作の詳細については、「[事前関連付け操作](pre-association-operations.md)」を参照してください。

<a href="" id="post-association-------"></a>**関連付け後の**   
IHV 拡張 DLL の後の接続フェーズは、関連付け後の操作を完了します。 関連付け後の操作の詳細については、「[関連付け後の操作](post-association-operations.md)」を参照してください。

オペレーティングシステムは、ネイティブ 802.11 IHV Extensions DLL の[*Dot11ExtIhvQueryUIRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_query_ui_request) ihv ハンドラー関数を呼び出して、カスタム UI を表示できるかどうかを照会します。 オペレーティングシステムは、 *connectionphase*パラメーターを使用して、接続プロセスの現在のフェーズを渡します。 カスタム UI を表示する必要がある場合、DLL は、p *Pihvuirequest*パラメーターを使用して、 [**DOT11EXT\_IHV\_UI\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11ext_ihv_ui_request)構造体を返します。

ネイティブ 802.11 IHV 拡張 DLL では、 [**DOT11EXT\_IHV\_UI\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11ext_ihv_ui_request)構造を使用して、次のデータを使用してカスタム UI を指定します。

-   ユーザーセッション識別子 (ID)。特定のユーザーコンテキストを識別するために使用されます。

-   特定の UI 要求を識別するグローバル一意識別子 (GUID)。

-   ネイティブ 802.11 IHV UI 拡張 DLL 内に実装されている**IWizardExtension** COM インターフェイスのクラス ID (CLSID)。 CLSID は、DLL によってサポートされる特定のカスタム UI を要求するために使用されます。

    **IWizardExtension** com インターフェイスの詳細については、「 [IWizardExtension com インターフェイス](https://go.microsoft.com/fwlink/p/?linkid=56607)」を参照してください。

-   独立系ハードウェアベンダー (IHV) によって定義され、指定された**IWizardExtension** COM インターフェイスによって処理される専用の形式のデータを格納するバッファー。 たとえば、バッファーには、カスタム UI 内に表示される既定値を含めることができます。

カスタム UI は、標準のネットワーク接続 UI 内の一連のウィザードページとして表示されます。 このプロセスの詳細については、「[ネットワーク接続ウィザードでカスタム UI ページを表示する](displaying-custom-ui-pages-within-the-network-connection-wizard.md)」を参照してください。

 

 





