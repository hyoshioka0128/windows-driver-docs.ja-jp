---
title: デバイスのインターフェイスに設定するプロパティの決定
description: デバイスのインターフェイスに設定するプロパティの決定
ms.assetid: ef261c1d-0715-4501-b2db-fab270cee010
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4c4097a329b550007745109afd6ca6752a11a98
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374242"
---
# <a name="determining-which-properties-are-set-for-a-device-interface"></a>デバイスのインターフェイスに設定するプロパティの決定


Windows Vista および以降のバージョンの Windows デバイスのインターフェイスを設定するプロパティを確認するのには、次の手順を実行します。

1.  呼び出す[ **SetupDiGetDeviceInterfacePropertyKeys** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertykeys)デバイス クラスの数のプロパティは設定を指定します。 次のパラメーター値を指定します。

    -   設定*DeviceInfoSet*デバイス インターフェイスのプロパティのキーの一覧を取得する対象のデバイス インターフェイスのインスタンスを含むデバイス情報のセットへのハンドル。
    -   設定*DeviceInterfaceData*へのポインター、 [ **SP_DEVICE_INTERFACE_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_device_interface_data)の一覧を取得する対象のデバイスのインターフェイスのインスタンスを表す構造体デバイス プロパティのキー。
    -   設定*PropertyKeyArray*に**NULL**します。
    -   設定*PropertyKeyCount*をゼロにします。
    -   設定*RequiredPropertyKeyCount* DWORD に型指定された変数へのポインター。
    -   フラグを 0 に設定します。

    この呼び出しに応答[ **SetupDiGetDeviceInterfacePropertyKeys**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertykeys)、 **SetupDiGetDeviceInterfacePropertyKeys**設定\* *RequiredPropertyKeyCount*デバイス インターフェイスに設定されているプロパティの数、エラー コード、ERROR_INSUFFICIENT_BUFFER ログに記録し、返します**FALSE**します。 後続の呼び出し[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)最近記録されたエラー コードを最大限に戻ります。

2.  呼び出す**SetupDiGetDeviceInterfacePropertyKeys**もう一度次の変更を除き、最初の呼び出しで指定された同じパラメーター値を提供します。
    -   設定*PropertyKeyArray*を[ **DEVPROPKEY**](https://docs.microsoft.com/windows-hardware/drivers/install/devpropkey)-要求されたプロパティのキーの配列を受け取るバッファーへの型指定されたポインター。
    -   設定*PropertyKeyCount* DEVPROPKEY に型指定された値で、サイズの*PropertyKeyArray*バッファー。 最初の呼び出し**SetupDiGetDeviceInterfacePropertyKeys**の必要なサイズを取得、 *PropertyKeyArray*内でバッファー \* *RequiredPropertyKeyCount*.

2 番目の呼び出しに場合**SetupDiGetDeviceInterfacePropertyKeys**成功すると、 **SetupDiGetDeviceInterfacePropertyKeys**で要求されたプロパティのキーの配列を返します、 *PropertyKeyArray*バッファー、セット\* *RequiredPropertyKeyCount*バッファー、および返します内のプロパティのキーの数に**TRUE**します。 関数呼び出しが失敗した場合、 **SetupDiGetDeviceInterfacePropertyKeys**返します**FALSE**への呼び出しと[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)はログに記録されたエラー コードを返します。

 

 





