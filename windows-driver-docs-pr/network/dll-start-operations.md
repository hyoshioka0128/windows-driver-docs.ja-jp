---
title: DLL 開始操作
description: DLL 開始操作
ms.assetid: cab7a4f9-35dc-44fc-bdd0-30bac8beb652
keywords:
- IHV Extensions DLL WDK ネイティブ802.11、開始操作
- IHV 拡張 DLL を開始しています
- ネイティブ 802.11 IHV 拡張 DLL WDK、開始操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 873b10569fde25ce9b4bf369532ba5188f04e46c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838133"
---
# <a name="dll-start-operations"></a>DLL 開始操作




 

IHV 拡張 DLL を読み込んだ直後に、オペレーティングシステムは、このシーケンスで次の IHV ハンドラー関数を呼び出します。

1.  オペレーティングシステムは、 [*Dot11ExtIhvGetVersionInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_get_version_info) ihv ハンドラー関数を呼び出して、IHV 拡張 DLL によってサポートされるインターフェイスのバージョンを確認します。 この関数には、 [**DOT11\_IHV\_VERSION\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11_ihv_version_info)構造体へのポインターが渡されます。この構造体は、サポートされている最小および最大のインターフェイスバージョンと共に DLL 形式になります。
    **注**  Windows Vista では、IHV 拡張 DLL は、DOT11\_IHV\_VERSION\_INFO 構造体の**DwVerMin**および**dwvermax**メンバーを0に設定する必要があります。

     

2.  オペレーティングシステムでサポートされているインターフェイスバージョンが IHV 拡張 DLL によってサポートされている場合、オペレーティングシステムは[*Dot11ExtIhvInitService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_service) IHV ハンドラー関数を呼び出して DLL を初期化します。

[*Dot11ExtIhvInitService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_service)が呼び出された場合、IHV 拡張 DLL は次のガイドラインに従う必要があります。

-   *PDot11ExtAPI*パラメーターには、 [**DOT11EXT\_api**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11ext_apis)構造体へのポインターが含まれています。これは、オペレーティングシステムでサポートされている IHV 拡張機能のアドレスで書式設定されています。 IHV 拡張 DLL は、 *pDot11ExtAPI*パラメーターによって参照される DOT11EXT\_api 構造体を、グローバルに宣言された DOT11EXT\_api 構造体にコピーする必要があります。

-   *PDot11IHVHandlers*パラメーターには、 [**DOT11EXT\_ihv\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11ext_ihv_handlers) handler 構造体へのポインターが含まれています。この構造体は、ihv Extensions DLL がサポートする ihv ハンドラー関数のアドレスと共に書式設定します。
    DLL  、DOT11EXT\_IHV\_ハンドラー構造体のいずれのメンバーも**NULL**に設定する**こと**はできません。

     

-   IHV 拡張 DLL は、 [*Dot11ExtIhvInitService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_service)から dll が返された後に、ihv ハンドラー関数の呼び出しの準備として、内部初期化とリソース割り当てを実行する必要があります。

IHV 拡張機能の詳細については、「[ネイティブ 802.11 Ihv 拡張関数](https://docs.microsoft.com/windows-hardware/drivers/network/native-802-11-ihv-extensibility-functions)」を参照してください。

IHV ハンドラー関数の詳細については、「[ネイティブ 802.11 Ihv ハンドラー関数](https://docs.microsoft.com/windows-hardware/drivers/network/native-802-11-ihv-handler-functions)」を参照してください。

 

 





