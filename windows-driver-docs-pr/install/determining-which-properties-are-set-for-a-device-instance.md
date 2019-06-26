---
title: デバイス インスタンスに設定するプロパティの決定
description: デバイス インスタンスに設定するプロパティの決定
ms.assetid: aeca4da5-9632-4523-aa2d-8d1c64b1eccc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a66cf363c690450895a432df3c2c9930864cf165
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374245"
---
# <a name="determining-which-properties-are-set-for-a-device-instance"></a>デバイス インスタンスに設定するプロパティの決定


Windows Vista および以降のバージョンの Windows デバイスのインスタンスを設定するプロパティを確認するのには、次の手順を実行します。

1.  呼び出す[ **SetupDiGetDevicePropertyKeys** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertykeys)デバイス インスタンスの数のプロパティは設定を指定します。 次のパラメーター値を指定します。

    -   設定*DeviceInfoSet*プロパティのキーの一覧を取得する対象のデバイスのインスタンスを含むデバイス情報のセットへのハンドル。
    -   設定*DeviceInfoData*へのポインター、 [ **SP_DEVINFO_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)プロパティのキーの一覧を取得する対象のデバイスのインスタンスを表す構造体です。
    -   設定*PropertyKeyArray*に**NULL**します。
    -   設定*PropertyKeyCount*をゼロにします。
    -   設定*RequiredPropertyKeyCount* DWORD に型指定された変数へのポインター。
    -   設定*フラグ*をゼロにします。

    呼び出しに応答[ **SetupDiGetDevicePropertyKeys**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertykeys)、 **SetupDiGetDevicePropertyKeys**設定\* *RequiredPropertyKeyCount*デバイス インスタンスに設定されているプロパティの数、エラー コード、ERROR_INSUFFICIENT_BUFFER ログに記録し、返します**FALSE**します。 後続の呼び出し[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)最近記録されたエラー コードを最大限に戻ります。

2.  呼び出す**SetupDiGetDevicePropertyKeys**もう一度次の変更を除き、最初の呼び出しで指定された同じパラメーター値を提供します。

    -   設定*PropertyKeyArray*として、 [ **DEVPROPKEY**](https://docs.microsoft.com/windows-hardware/drivers/install/devpropkey)-要求されたプロパティのキーの配列を受け取るバッファーへの型指定されたポインター。
    -   設定*PropertyKeyCount* DEVPROPKEY に型指定された値で、サイズの*PropertyKeyArray*バッファー。 最初の呼び出し**SetupDiGetDevicePropertyKeys**の必要なサイズを取得、 *PropertyKeyArray*内でバッファー \* *RequiredPropertyKeyCount*します。

2 番目の呼び出しに場合**SetupDiGetDevicePropertyKeys**成功すると、 **SetupDiGetDevicePropertyKeys**で要求されたプロパティのキーの配列を返します、 *PropertyKeyArray*バッファー、セット\* *RequiredPropertyKeyCount*バッファー、および返します内のプロパティのキーの数に**TRUE**します。 関数呼び出しが失敗した場合、 **SetupDiGetDevicePropertyKeys**返します**FALSE**を呼び出すと[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=74036)はログに記録されたエラー コードを返します。

 

 





