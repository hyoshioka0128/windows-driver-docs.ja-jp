---
title: デバイス クラスのプロパティ値の設定
description: デバイス クラスのプロパティ値の設定
ms.assetid: a1d6908d-e43a-413d-965b-3af226d5c26f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03ece74b9a63a53d7021d2a3ea2b04b9fb517c65
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348929"
---
# <a name="setting-a-device-class-property-value"></a>デバイス クラスのプロパティ値の設定


次のトピックでは、Windows Vista および以降のバージョンの Windows でのデバイス クラスのプロパティ値を設定する方法について説明します。

[ローカル コンピューター上のデバイス クラスのプロパティ値の設定](#setting-a-device-class-property-value-on-a-local-computer)

[リモート コンピューター上のデバイス クラスのプロパティ値の設定](#setting-a-device-class-property-value-on-a-remote-computer)

### <a href="" id="setting-a-device-class-property-value-on-a-local-computer"></a> ローカル コンピューター上のデバイス クラスのプロパティ値の設定

デバイス クラスのプロパティの値を設定するには、呼び出す[ **SetupDiSetClassProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff552128)し、次のパラメーター値を指定します。

-   設定*ClassGuid*を識別する GUID へのポインター、[デバイス セットアップ クラス](device-setup-classes.md)または[デバイス インターフェイス クラス](device-interface-classes.md)クラスのプロパティを設定します。

-   設定*PropertyKey*へのポインター、 [ **DEVPROPKEY** ](https://msdn.microsoft.com/library/windows/hardware/ff543544)を設定するプロパティを表す構造体です。

-   設定*PropertyType*へのポインターを[ **DEVPROPTYPE**](https://msdn.microsoft.com/library/windows/hardware/ff543546)-型指定された変数を設定するプロパティの識別子のデータ型のプロパティを提供します。

-   設定*PropertyBuffer*プロパティの値を格納しているバッファーへのポインター。

-   設定*PropertyBufferSize*プロパティの値のバイト単位のサイズにします。

-   設定*RequiredSize* DWORD に型指定された変数にします。

-   デバイスのクラスが、デバイス セットアップ クラスの場合は、設定*フラグ*DICLASSPROP_INSTALLER にします。 それ以外の場合、デバイスのクラスがデバイスのインターフェイス クラスの場合は、設定*フラグ*DICLASSPROP_INTERFACE にします。

呼び出し[ **SetupDiSetClassProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff552128)成功すると、 **SetupDiSetClassProperty**デバイス クラスのプロパティを設定し、返します**TRUE**. 関数呼び出しが失敗した場合、 **SetupDiSetClassProperty**返します**FALSE**への呼び出しと[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)はログに記録されたエラー コードを返します。

### <a href="" id="setting-a-device-class-property-value-on-a-remote-computer"></a> リモート コンピューター上のデバイス クラスのプロパティ値の設定

リモート コンピューター上のデバイス クラスのプロパティ値を設定するに記載されている手順に従います[ローカル コンピューター上のデバイス クラスのプロパティ値の設定](#setting-a-device-class-property-value-on-a-local-computer)で、次の変更。

-   呼び出す[ **SetupDiSetClassPropertyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff552132)の代わりに**SetupDiSetClassProperty**します。

-   だけでなく、パラメーターの値を両方**SetupDiSetClassPropertyEx**と**SetupDiSetClassProperty**指定を必要と、 *MachineName*パラメーターUNC 名を含む NULL で終わる文字列へのポインターに設定する必要がある必要がありますを含め、 \\ \\のコンピューターのプレフィックス。

 

 





