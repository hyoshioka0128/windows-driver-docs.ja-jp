---
title: デバイス インターフェイス プロパティ値の取得
description: デバイス インターフェイス プロパティ値の取得
ms.assetid: 2a845adc-6965-420d-9e0a-20935d20577a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ab588415d95e9a5910679cb982c8297305f580f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363339"
---
# <a name="retrieving-a-device-interface-property-value"></a>デバイス インターフェイス プロパティ値の取得


以降では、Windows Vista では、次の手順の値を取得する、[デバイス インターフェイス プロパティ](https://msdn.microsoft.com/library/windows/hardware/ff541409):

1.  呼び出す[ **SetupDiGetDeviceInterfaceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551122)データ型とプロパティの値のバイト単位のサイズを決定します。 次のパラメーター値を指定します。

    -   設定*DeviceInfoSet*デバイス インターフェイスのプロパティのキーの一覧を取得する対象のデバイスのインターフェイスが含まれるデバイス情報のセットへのハンドル。
    -   設定*DeviceInterfaceData*へのポインター、 [ **SP_DEVICE_INTERFACE_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552342)デバイスの一覧を取得する対象のデバイスのインターフェイスを表す構造体プロパティのキー。
    -   設定*PropertyKey*へのポインターを[ **DEVPROPKEY** ](https://msdn.microsoft.com/library/windows/hardware/ff543544)プロパティを表す構造体です。
    -   設定*PropertyType*へのポインターを[ **DEVPROPKEY**](https://msdn.microsoft.com/library/windows/hardware/ff543544)-型指定された変数。
    -   設定*PropertyBuffer*に**NULL**します。
    -   設定*PropertyBufferSize*をゼロにします。
    -   設定*RequiredSize* DWORD に型指定された変数にします。
    -   フラグを 0 に設定します。

    最初の呼び出しに応答[ **SetupDiGetDeviceInterfaceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551122)、 **SetupDiGetDeviceInterfaceProperty**設定\* *RequiredSize*プロパティ値を取得するために必要なバッファーのバイト単位でログ、ERROR_INSUFFICIENT_BUFFER エラー コードのサイズにし、返します**FALSE**します。 後続の呼び出し[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)最近記録されたエラー コードを最大限に戻ります。

2.  呼び出す**SetupDiGetDeviceInterfaceProperty**もう一度次の変更を除き、最初の呼び出しに指定された同じパラメーター値を提供します。
    -   設定*PropertyBuffer*プロパティの値を受け取るバッファーへのポインター。
    -   設定*PropertyBufferSize* (バイト単位)、必要なサイズの*PropertyBuffer*バッファー。 最初の呼び出し**SetupDiGetDeviceInterfaceProperty**の必要なサイズを取得、 *PropertyBuffer*内でバッファー \* *RequiredSize*します。

2 番目の呼び出しに場合**SetupDiGetDeviceInterfaceProperty**成功すると、 **SetupDiGetDeviceInterfaceProperty**設定\* *PropertyType*に、プロパティの識別子のデータ型のプロパティの設定、 *PropertyBuffer* 、プロパティの値を設定するバッファー \* *RequiredSize*プロパティのバイト単位のサイズ値を取得したを返す**TRUE**します。 関数呼び出しが失敗した場合、 **SetupDiGetDeviceInterfaceProperty**返します**FALSE**への呼び出しと[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)はログに記録されたエラー コードを返します。

 

 





