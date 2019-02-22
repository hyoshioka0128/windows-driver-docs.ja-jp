---
title: デバイス インスタンスのプロパティ値を取得します。
description: デバイス インスタンスのプロパティ値を取得します。
ms.assetid: 4cec9132-5a28-492d-bbb1-39e388413ad0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d14fe31c3d4d79cd6b8b8f4fab68df2e7a44b7e3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560198"
---
# <a name="retrieving-a-device-instance-property-value"></a>デバイス インスタンスのプロパティ値を取得します。


Windows Vista でのデバイス インスタンス プロパティの値と以降のバージョンの Windows を取得するには、次の手順に従います。

1.  呼び出す[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963)データ型とプロパティの値のバイト単位のサイズを決定します。 次のパラメーター値を指定します。

    -   設定*DeviceInfoSet*プロパティを取得する対象のデバイスのインスタンスを含むデバイス情報のセットへのハンドル。
    -   設定*DeviceInfoData*へのポインター、 [ **SP_DEVINFO_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552344)プロパティを取得する対象のデバイスのインスタンスを表す構造体です。
    -   設定*PropertyKey*へのポインターを[ **DEVPROPKEY** ](https://msdn.microsoft.com/library/windows/hardware/ff543544)プロパティを表す構造体です。
    -   設定*PropertyType*へのポインターを[ **DEVPROPTYPE**](https://msdn.microsoft.com/library/windows/hardware/ff543546)-型指定された変数。
    -   設定*PropertyBuffer*に**NULL**します。
    -   設定*PropertyBufferSize*をゼロにします。
    -   設定*RequiredSize* DWORD に型指定された変数へのポインター。
    -   設定*フラグ*をゼロにします。

    最初の呼び出しに応答[ **SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)、 **SetupDiGetDeviceProperty**設定\* *RequiredSize*プロパティ値を取得するために必要なバッファーのバイト単位でログ、ERROR_INSUFFICIENT_BUFFER エラー コードのサイズにし、返します**FALSE**します。 後続の呼び出し[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)最近記録されたエラー コードを最大限に戻ります。

2.  呼び出す**SetupDiGetDeviceProperty**もう一度次の変更を除き、最初の呼び出しで指定された同じパラメーター値を提供します。
    -   設定*PropertyBuffer*プロパティの値を受け取るバッファーへのポインター。
    -   設定*PropertyBufferSize* (バイト単位)、必要なサイズの*PropertyBuffer*バッファー。 最初の呼び出し**SetupDiGetDeviceProperty**の必要なサイズを取得、 *PropertyBuffer*内でバッファー \* *RequiredSize*します。

2 番目の呼び出しに場合**SetupDiGetDeviceProperty**成功すると、 **SetupDiGetDeviceProperty**設定\* *PropertyType*プロパティ データ型にプロパティ値を返します、プロパティの識別子、 *PropertyBuffer*バッファー、セット\* *RequiredSize*サイズ (バイト単位) のプロパティの値でした取得し、返します**TRUE**します。 関数呼び出しが失敗した場合、 **SetupDiGetDeviceProperty**返します**FALSE**への呼び出しと[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)はログに記録されたエラー コードを返します。

 

 





