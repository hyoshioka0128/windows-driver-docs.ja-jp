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
ms.openlocfilehash: 4f74c41200f00c7edcb030ebaa2e3c73b5cee7c5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325013"
---
# <a name="initializing-a-miniport-driver"></a>ミニポート ドライバーの初期化



ネットワーク デバイスが使用可能になるときに、システムは、NDIS ミニポート ドライバー (ドライバーがまだ読み込まれていない) 場合、デバイスを管理するを読み込みます。 すべてのミニポート ドライバーを提供する必要があります、 [DriverEntry](https://msdn.microsoft.com/library/windows/hardware/ff544113)関数。 システム コール**DriverEntry**ドライバーが読み込まれた後です。 **DriverEntry** NDIS (サポートされている NDIS バージョンとドライバーのエントリ ポイントを含む) を使用して、ミニポート ドライバーの特性を登録します。

システムは、2 つの引数を渡します[DriverEntry](https://msdn.microsoft.com/library/windows/hardware/ff544113):

-   I/O システムによって作成されたドライバー オブジェクトへのポインター。

-   ドライバー固有のパラメーターを格納する場所を指定するレジストリ パスへのポインター。

[DriverEntry](https://msdn.microsoft.com/library/windows/hardware/ff544113)、ミニポート ドライバーがこれらのポインターの両方への呼び出しに渡す、 [NdisMRegisterMiniportDriver](https://msdn.microsoft.com/library/windows/hardware/ff563654)関数。 ミニポート ドライバーは、標準のセットをエクスポート*MiniportXxx*関数で、エントリ ポイントを格納することにより、 [ **NDIS\_ミニポート\_ドライバー\_特性** ](https://msdn.microsoft.com/library/windows/hardware/ff565958)構造と構造体を渡す**NdisMRegisterMiniportDriver**します。 

**DriverEntry**ミニポート ドライバーへの呼び出しによって返される値を返します**NdisMRegisterMiniportDriver**します。

ミニポート ドライバーで必要なその他の個々 のドライバーの初期化を実行も[DriverEntry](https://msdn.microsoft.com/library/windows/hardware/ff544113)します。 ドライバーのアダプター固有の初期化を実行する、 [ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数。 アダプターの初期化の詳細については、次を参照してください。 [、アダプターの初期化](initializing-a-miniport-adapter.md)します。

[DriverEntry](https://msdn.microsoft.com/library/windows/hardware/ff544113)割り当てることができます、 [ **NDIS\_ミニポート\_ドライバー\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565958) NDIS ライブラリをコピーするために、スタックの構造体独自のストレージに関連する情報。 **DriverEntry**でこの構造体のメモリをオフにする必要があります[NdisZeroMemory](https://msdn.microsoft.com/library/windows/hardware/ff564698)そのメンバー内のドライバーが指定した値を設定する前にします。 **MajorNdisVersion**と**MinorNdisVersion**メンバーは、ドライバーがサポートする NDIS のメジャーおよびマイナーのバージョンを含める必要があります。 各 Xxx の**ハンドラー**特性構造体のメンバー **DriverEntry**のドライバーが指定したエントリ ポイントを設定する必要があります*MiniportXxx*関数、またはメンバーである必要があります**NULL**します。

NDIS の呼び出しを省略可能なサービスを構成するミニポート ドライバーを有効にする、 [MiniportSetOptions](https://msdn.microsoft.com/library/windows/hardware/ff559443)ミニポート ドライバーの呼び出しのコンテキスト内で関数[NdisMRegisterMiniportDriver](https://msdn.microsoft.com/library/windows/hardware/ff563654)します。 省略可能なサービスの詳細については、次を参照してください。[省略可能なミニポート ドライバー サービスを構成する](configuring-optional-miniport-driver-services.md)します。

呼び出すドライバー [NdisMRegisterMiniportDriver](https://msdn.microsoft.com/library/windows/hardware/ff563654) NDIS を呼び出すために準備する必要があります、 [ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数の後にいつでも**DriverEntry**を返します。 そのような情報が必要十分なインストールと構成、レジストリに格納されているまたはへの呼び出しから使用可能な**NdisXxx**ドライバーを任意の NIC に固有のリソースを設定するバスの種類に固有の構成関数ネットワーク I/O 操作を実行する必要があります。

最終的に、ミニポート ドライバーを呼び出す必要があります[ **NdisMDeregisterMiniportDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff563578)呼び出すことによって、割り当てられたリソースを解放する[ **NdisMRegisterMiniportDriver**](https://msdn.microsoft.com/library/windows/hardware/ff563654). 呼び出した後、ドライバーの初期化に失敗した場合**NdisMRegisterMiniportDriver**ドライバーを呼び出すことができますが成功した**NdisMDeregisterMiniportDriver**内から[DriverEntry](https://msdn.microsoft.com/library/windows/hardware/ff544113). ミニポート ドライバーがで割り当てるドライバー固有のリソースを解放する必要がありますそれ以外の場合、その[ *MiniportDriverUnload* ](https://msdn.microsoft.com/library/windows/hardware/ff559378)関数。 つまり NdisMRegisterMiniportDriver に NDIS_STATUS_SUCCESS、返さない場合、 **DriverEntry**リソースを解放する必要があります制御を返す前に、割り当てられました。 このような場合、ドライバーは読み込まれません。 詳細については、次を参照してください。[ミニポート ドライバーをアンロード](unloading-a-miniport-driver.md)します。

 

 





