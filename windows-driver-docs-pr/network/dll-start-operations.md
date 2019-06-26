---
title: DLL 開始操作
description: DLL 開始操作
ms.assetid: cab7a4f9-35dc-44fc-bdd0-30bac8beb652
keywords:
- IHV 拡張 DLL WDK ネイティブ 802.11、開始操作
- IHV 拡張 DLL の開始
- ネイティブの 802.11 IHV 拡張 DLL の WDK の操作を開始します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2542c6bf488fa0d4576c235a5ece19ac1c332ce3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386557"
---
# <a name="dll-start-operations"></a>DLL 開始操作




 

IHV 拡張機能の DLL を読み込み、直後には、オペレーティング システムは、このシーケンスで、次の IHV ハンドラー関数を呼び出します。

1.  オペレーティング システムの呼び出し、 [ *Dot11ExtIhvGetVersionInfo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_get_version_info) IHV 拡張機能の DLL によってサポートされているインターフェイスのバージョンを決定する IHV ハンドラー関数。 この関数へのポインターを渡される、 [ **DOT11\_IHV\_バージョン\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/ns-wlanihv-_dot11_ihv_version_info) DLL が最小値と最大のインターフェイスのバージョンを使用した形式の構造サポートしています。
    **注**  Windows Vista の IHV 拡張機能の DLL を設定する必要があります、 **dwVerMin**と**dwVerMax** 、DOT11 のメンバー\_IHV\_のバージョン\_0 に情報構造体。

     

2.  IHV 拡張機能の DLL は、オペレーティング システムでサポートされているインターフェイスのバージョンをサポートする場合、オペレーティング システムの呼び出し、 [ *Dot11ExtIhvInitService* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_init_service) IHV ハンドラー関数を DLL を初期化します。

IHV 拡張機能の DLL が次のガイドラインに従う必要がありますと[ *Dot11ExtIhvInitService* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_init_service)が呼び出されます。

-   *PDot11ExtAPI*パラメーターにはへのポインターが含まれています、 [ **DOT11EXT\_API** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/ns-wlanihv-_dot11ext_apis) IHV 機能拡張のアドレスでフォーマットされた構造体オペレーティング システムでサポートされている機能です。 IHV 拡張機能の DLL は、DOT11EXT をコピーする必要があります\_によって参照されている API の構造体、 *pDot11ExtAPI*パラメーターをグローバルに宣言された DOT11EXT\_API 構造体。

-   *PDot11IHVHandlers*パラメーターにはへのポインターが含まれています、 [ **DOT11EXT\_IHV\_ハンドラー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/ns-wlanihv-_dot11ext_ihv_handlers)構造を IHV 拡張 DLLサポートされている IHV ハンドラー関数のアドレスを持つ形式。
    **注**  DLL は、DOT11EXT のメンバーのいずれかを設定しない必要があります\_IHV\_ハンドラーが構造体を**NULL**します。

     

-   IHV 拡張機能の DLL から DLL を返します後に、その IHV ハンドラー関数を呼び出すのための準備の任意の内部の初期化とリソース割り当てを実行する必要があります[ *Dot11ExtIhvInitService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_init_service)します。

IHV 拡張機能の詳細については、次を参照してください。 [802.11 IHV 拡張関数をネイティブ](https://docs.microsoft.com/windows-hardware/drivers/network/native-802-11-ihv-extensibility-functions)します。

IHV ハンドラー関数の詳細については、次を参照してください。 [802.11 IHV ハンドラー関数をネイティブ](https://docs.microsoft.com/windows-hardware/drivers/network/native-802-11-ihv-handler-functions)します。

 

 





