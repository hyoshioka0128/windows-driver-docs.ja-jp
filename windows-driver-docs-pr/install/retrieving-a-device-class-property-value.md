---
title: デバイス クラスのプロパティ値を取得します。
description: デバイス クラスのプロパティ値を取得します。
ms.assetid: 50b16bd9-7f38-4128-af8f-8b39b099931f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a305bdf1de39ecbc277910b808dd51f00ac816d2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528967"
---
# <a name="retrieving-a-device-class-property-value"></a>デバイス クラスのプロパティ値を取得します。


次のトピックでは、Windows Vista 以降のバージョンの Windows でのデバイス クラス プロパティ値を取得する方法について説明します。

[ローカル コンピューター上でデバイス クラスのプロパティの値を取得します。](#retrieving-a-device-class-property-value-on-a-local-computer)

[リモート コンピューター上でデバイス クラスのプロパティの値を取得します。](#retrieving-a-device-class-property-value-on-a-remote-computer)

### <a href="" id="retrieving-a-device-class-property-value-on-a-local-computer"></a> ローカル コンピューター上でデバイス クラスのプロパティの値を取得します。

ローカル コンピューター上のデバイス クラスのプロパティの値を取得するには、次の手順に従います。

1.  呼び出す[ **SetupDiGetClassProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551086)データ型とプロパティの値のバイト単位のサイズを決定します。 次のパラメーター値を指定します。

    -   設定*ClassGuid*を識別する GUID へのポインター、[デバイス セットアップ クラス](device-setup-classes.md)または[デバイス インターフェイス クラス](device-interface-classes.md)をデバイスに設定されているクラスのプロパティを取得します。クラス。
    -   設定*PropertyKey*へのポインターを[ **DEVPROPKEY** ](https://msdn.microsoft.com/library/windows/hardware/ff543544)プロパティを表す構造体です。
    -   設定*PropertyType*へのポインターを[ **DEVPROPTYPE**](https://msdn.microsoft.com/library/windows/hardware/ff543546)-型指定された変数。
    -   設定*PropertyBuffer*に**NULL**します。
    -   設定*PropertyBufferSize*をゼロにします。
    -   設定*RequiredSize* DWORD に型指定された変数にします。
    -   デバイスのクラスが、デバイス セットアップ クラスの場合は、設定*フラグ*DICLASSPROP_INSTALLER にします。 それ以外の場合、デバイスのクラスがデバイスのインターフェイス クラスの場合は、設定*フラグ*DICLASSPROP_INTERFACE にします。

    この最初の呼び出しに応答[ **SetupDiGetClassProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551086)、 **SetupDiGetClassProperty**設定\* *RequiredSize*プロパティ値を取得するために必要なバッファーのバイト単位でログ、ERROR_INSUFFICIENT_BUFFER エラー コードのサイズにし、返します**FALSE**します。 後続の呼び出し[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)最近記録されたエラー コードを最大限に戻ります。

2.  呼び出す**SetupDiGetClassProperty**もう一度と、次の変更を除き、最初の呼び出しで指定された同じパラメーターを指定します。
    -   設定*PropertyBuffer*プロパティの値を受け取るバッファーへのポインター。
    -   設定*PropertyBufferSize* (バイト単位)、必要なサイズの*PropertyBuffer*バッファー。 最初の呼び出し**SetupDiGetClassProperty**の必要なサイズを取得、 *PropertyBuffer*内でバッファー \* *RequiredSize*します。

場合は、2 つ目の呼び出し**SetupDiGetClassProperty**成功すると、 **SetupDiGetClassProperty**設定\* *PropertyType*プロパティ データ型識別子プロパティの設定、 *PropertyBuffer* 、プロパティの値を設定するバッファー \* *RequiredSize*サイズ (バイト単位) のプロパティの値を取得したを返す**TRUE**します。 関数呼び出しが失敗した場合、 **SetupDiGetDeviceProperty**返します**FALSE**への呼び出しと[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)はログに記録されたエラー コードを返します。

### <a href="" id="retrieving-a-device-class-property-value-on-a-remote-computer"></a> リモート コンピューター上でデバイス クラスのプロパティの値を取得します。

リモート コンピューター上でデバイス クラスのプロパティの値を取得するには、同じ手順に従ってに説明されている[ローカル コンピューター上でデバイス クラスのプロパティの値を取得する](#retrieving-a-device-class-property-value-on-a-local-computer)で、次の変更。

-   呼び出す[ **SetupDiGetClassPropertyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551090)の代わりに**SetupDiGetClassProperty**します。

-   だけでなく、パラメーターの値を**SetupDiGetDevicePropertyEx**と**SetupDiGetClassProperty**指定を必要と両方、 *MachineName*パラメーターUNC 名を含む NULL で終わる文字列へのポインターに設定する必要がある必要がありますを含め、 \\ \\のコンピューターのプレフィックス。

 

 





