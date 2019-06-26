---
title: ミニポート ドライバーの初期化
description: ミニポート ドライバーの初期化
ms.assetid: cda2437c-b292-4d21-b200-89c7b55cd46c
keywords:
- ミニポート ドライバー WDK ネットワーク、初期化しています
- ミニポート ドライバーの初期化
- NDIS ミニポート ドライバー WDK、初期化しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b8c3e70b744f0dbae050466f6587b1aab52fa05
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381328"
---
# <a name="initializing-a-miniport-driver"></a>ミニポート ドライバーの初期化



ネットワーク デバイスが使用可能になるときに、システムは、NDIS ミニポート ドライバー (ドライバーがまだ読み込まれていない) 場合、デバイスを管理するを読み込みます。 すべてのミニポート ドライバーを提供する必要があります、 [DriverEntry](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)関数。 システム コール**DriverEntry**ドライバーが読み込まれた後です。 **DriverEntry** NDIS (サポートされている NDIS バージョンとドライバーのエントリ ポイントを含む) を使用して、ミニポート ドライバーの特性を登録します。

システムは、2 つの引数を渡します[DriverEntry](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize):

-   I/O システムによって作成されたドライバー オブジェクトへのポインター。

-   ドライバー固有のパラメーターを格納する場所を指定するレジストリ パスへのポインター。

[DriverEntry](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)、ミニポート ドライバーがこれらのポインターの両方への呼び出しに渡す、 [NdisMRegisterMiniportDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)関数。 ミニポート ドライバーは、標準のセットをエクスポート*MiniportXxx*関数で、エントリ ポイントを格納することにより、 [ **NDIS\_ミニポート\_ドライバー\_特性** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_driver_characteristics)構造と構造体を渡す**NdisMRegisterMiniportDriver**します。 

**DriverEntry**ミニポート ドライバーへの呼び出しによって返される値を返します**NdisMRegisterMiniportDriver**します。

ミニポート ドライバーで必要なその他の個々 のドライバーの初期化を実行も[DriverEntry](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)します。 ドライバーのアダプター固有の初期化を実行する、 [ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数。 アダプターの初期化の詳細については、次を参照してください。 [、アダプターの初期化](initializing-a-miniport-adapter.md)します。

[DriverEntry](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)割り当てることができます、 [ **NDIS\_ミニポート\_ドライバー\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_driver_characteristics) NDIS ライブラリをコピーするために、スタックの構造体独自のストレージに関連する情報。 **DriverEntry**でこの構造体のメモリをオフにする必要があります[NdisZeroMemory](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiszeromemory)そのメンバー内のドライバーが指定した値を設定する前にします。 **MajorNdisVersion**と**MinorNdisVersion**メンバーは、ドライバーがサポートする NDIS のメジャーおよびマイナーのバージョンを含める必要があります。 各 Xxx の**ハンドラー**特性構造体のメンバー **DriverEntry**のドライバーが指定したエントリ ポイントを設定する必要があります*MiniportXxx*関数、またはメンバーである必要があります**NULL**します。

NDIS の呼び出しを省略可能なサービスを構成するミニポート ドライバーを有効にする、 [MiniportSetOptions](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)ミニポート ドライバーの呼び出しのコンテキスト内で関数[NdisMRegisterMiniportDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)します。 省略可能なサービスの詳細については、次を参照してください。[省略可能なミニポート ドライバー サービスを構成する](configuring-optional-miniport-driver-services.md)します。

呼び出すドライバー [NdisMRegisterMiniportDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver) NDIS を呼び出すために準備する必要があります、 [ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数の後にいつでも**DriverEntry**を返します。 そのような情報が必要十分なインストールと構成、レジストリに格納されているまたはへの呼び出しから使用可能な**NdisXxx**ドライバーを任意の NIC に固有のリソースを設定するバスの種類に固有の構成関数ネットワーク I/O 操作を実行する必要があります。

最終的に、ミニポート ドライバーを呼び出す必要があります[ **NdisMDeregisterMiniportDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismderegisterminiportdriver)呼び出すことによって、割り当てられたリソースを解放する[ **NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver). 呼び出した後、ドライバーの初期化に失敗した場合**NdisMRegisterMiniportDriver**ドライバーを呼び出すことができますが成功した**NdisMDeregisterMiniportDriver**内から[DriverEntry](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize). ミニポート ドライバーがで割り当てるドライバー固有のリソースを解放する必要がありますそれ以外の場合、その[ *MiniportDriverUnload* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_unload)関数。 つまり NdisMRegisterMiniportDriver に NDIS_STATUS_SUCCESS、返さない場合、 **DriverEntry**リソースを解放する必要があります制御を返す前に、割り当てられました。 このような場合、ドライバーは読み込まれません。 詳細については、次を参照してください。[ミニポート ドライバーをアンロード](unloading-a-miniport-driver.md)します。

 

 





