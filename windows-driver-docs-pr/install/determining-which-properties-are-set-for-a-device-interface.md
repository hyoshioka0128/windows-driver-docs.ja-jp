---
title: プロパティの決定が、デバイス インターフェイスの設定します。
description: プロパティの決定が、デバイス インターフェイスの設定します。
ms.assetid: ef261c1d-0715-4501-b2db-fab270cee010
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1cba3efcfc8115e991f93b436d1c2a9c3744b7f6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550413"
---
# <a name="determining-which-properties-are-set-for-a-device-interface"></a>プロパティの決定が、デバイス インターフェイスの設定します。


Windows Vista および以降のバージョンの Windows デバイスのインターフェイスを設定するプロパティを確認するのには、次の手順を実行します。

1.  呼び出す[ **SetupDiGetDeviceInterfacePropertyKeys** ](https://msdn.microsoft.com/library/windows/hardware/ff551959)デバイス クラスの数のプロパティは設定を指定します。 次のパラメーター値を指定します。

    -   設定*DeviceInfoSet*デバイス インターフェイスのプロパティのキーの一覧を取得する対象のデバイス インターフェイスのインスタンスを含むデバイス情報のセットへのハンドル。
    -   設定*DeviceInterfaceData*へのポインター、 [ **SP_DEVICE_INTERFACE_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552342)の一覧を取得する対象のデバイスのインターフェイスのインスタンスを表す構造体デバイス プロパティのキー。
    -   設定*PropertyKeyArray*に**NULL**します。
    -   設定*PropertyKeyCount*をゼロにします。
    -   設定*RequiredPropertyKeyCount* DWORD に型指定された変数へのポインター。
    -   フラグを 0 に設定します。

    この呼び出しに応答[ **SetupDiGetDeviceInterfacePropertyKeys**](https://msdn.microsoft.com/library/windows/hardware/ff551959)、 **SetupDiGetDeviceInterfacePropertyKeys**設定\* *RequiredPropertyKeyCount*デバイス インターフェイスに設定されているプロパティの数、エラー コード、ERROR_INSUFFICIENT_BUFFER ログに記録し、返します**FALSE**します。 後続の呼び出し[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)最近記録されたエラー コードを最大限に戻ります。

2.  呼び出す**SetupDiGetDeviceInterfacePropertyKeys**もう一度次の変更を除き、最初の呼び出しで指定された同じパラメーター値を提供します。
    -   設定*PropertyKeyArray*を[ **DEVPROPKEY**](https://msdn.microsoft.com/library/windows/hardware/ff543544)-要求されたプロパティのキーの配列を受け取るバッファーへの型指定されたポインター。
    -   設定*PropertyKeyCount* DEVPROPKEY に型指定された値で、サイズの*PropertyKeyArray*バッファー。 最初の呼び出し**SetupDiGetDeviceInterfacePropertyKeys**の必要なサイズを取得、 *PropertyKeyArray*内でバッファー \* *RequiredPropertyKeyCount*.

2 番目の呼び出しに場合**SetupDiGetDeviceInterfacePropertyKeys**成功すると、 **SetupDiGetDeviceInterfacePropertyKeys**で要求されたプロパティのキーの配列を返します、 *PropertyKeyArray*バッファー、セット\* *RequiredPropertyKeyCount*バッファー、および返します内のプロパティのキーの数に**TRUE**します。 関数呼び出しが失敗した場合、 **SetupDiGetDeviceInterfacePropertyKeys**返します**FALSE**への呼び出しと[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)はログに記録されたエラー コードを返します。

 

 





