---
title: デバイスのソフトウェア キーのレジストリ値の変更
description: デバイスのソフトウェア キーのレジストリ値の変更
ms.assetid: 4DBDB53D-CA64-4c19-84A5-FBE1529FD0C5
keywords:
- レジストリ WDK デバイスのインストール、デバイスのソフトウェア キーのレジストリ値を変更します。
- WDK デバイスのインストール、デバイス ソフトウェアのキー値のレジストリを変更します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7750413002377ad67d9ff3206ba8041e997a1f87
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378353"
---
# <a name="modifying-registry-values-in-a-devices-software-key"></a>デバイスのソフトウェア キーのレジストリ値の変更


次のレジストリ エントリの値を変更する必要があります (*デバイス プロパティ*) で、デバイスの*ソフトウェア キー*:

-   DriverDate

-   DriverDateData

-   DriverDesc

-   DriverVersion

-   次のよう

-   InfSection

-   InfSectionExt

-   MatchingDeviceId

-   ProviderName

-   EnumPropPages32

これらのデバイス プロパティは、デバイスのインストール状態を表します。 これらのプロパティの直接的な変更には、デバイスのインストール状態が無効になる可能性があります。 関連する情報を変更するなど、 [INF ファイル](inf-files.md)デバイスとドライバーの署名情報などのプロパティに関連付けられているドライバー ファイルに関する情報が無効になります。 ドライバーのバージョンまたはドライバーの日付を変更すると、Windows 更新プログラム機能が壊れる可能性があります。

**注**  以降 Windows Vista では、オペレーティング システムで「インストール時のみ」は、これらのプロパティに関するアクセス制限です。 互換性のため、値を複製することができ、デバイスのインストール中に値の直接的な変更では内部状態には影響しません。

 

デバイスのソフトウェア キーの場合は、その他のレジストリ エントリの値を安全に変更するには、次のガイドラインに従います。

-   使用[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963)と[ **SetupDiSetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff552163)標準またはカスタム プロパティを取得および設定します。

    詳細については、次を参照してください。[デバイス ドライバーのプロパティへのアクセス](accessing-device-driver-properties.md)します。

-   オペレーティング システムに予約されていないデバイス プロパティのみを設定します。

    たとえば、ユーザーに表示されているデバイスの名前を変更するに次のように変更します。 その[ **DEVPKEY_Device_FriendlyName** ](https://msdn.microsoft.com/library/windows/hardware/ff542502)デバイス プロパティ。

 

 





