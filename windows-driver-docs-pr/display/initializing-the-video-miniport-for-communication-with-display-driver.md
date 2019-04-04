---
title: /表示のビデオのミニポート ドライバーの通信を初期化しています
description: ビデオのミニポートをディスプレイ ドライバーとの通信を初期化しています
ms.assetid: 73ba423c-7ebc-4a07-aed0-d2e33f11b878
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000 では、初期化しています
- ビデオのミニポート ドライバーの初期化
- HwVidInitialize
- one-time initialization WDK ビデオのミニポート
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 898cf7e25e1eda84d8ef0ff432c07609cac6f84a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539363"
---
# <a name="initializing-the-video-miniport-for-communication-with-display-driver"></a>ビデオのミニポートをディスプレイ ドライバーとの通信を初期化しています

各アダプターの PnP マネージャーによって検出され、正常に構成されているミニポート ドライバーで、ミニポート ドライバーの[ *HwVidInitialize* ](https://msdn.microsoft.com/library/windows/hardware/ff567345)関数は、対応する、ディスプレイ ドライバーが呼び出されます読み込まれます。 *HwVidInitialize*ソフトウェアの状態情報を初期化することができますが、アダプターの表示状態を設定しないでください。 戻り時にから*HwVidInitialize*、アダプターは、ミニポート ドライバーからの戻り値のと同じ状態に設定する必要があります[ *HwVidResetHw* ](https://msdn.microsoft.com/library/windows/hardware/ff567363)ルーチン。 詳細については*HwVidResetHw*を参照してください[ビデオのミニポート ドライバーのアダプターをリセットする](resetting-the-adapter-in-video-miniport-drivers.md)します。

必要に応じて、ミニポート ドライバーの*HwVidInitialize*関数は、アダプターによって延期されましたの one-time initialization 操作を実行できるその*HwVidFindAdapter*関数。 たとえば、ミニポート ドライバーがアダプター上のマイクロ コードの読み込みを延期しが可能性があります、 *HwVidInitialize*関数呼び出し[ **VideoPortGetRegistryParameters**](https://msdn.microsoft.com/library/windows/hardware/ff570316)します。

ときに、 *HwVidInitialize*します。 参照してください[ビデオの要求を処理する (Windows 2000 モデル)](processing-video-requests--windows-2000-model-.md)詳細についてはします。

通常、ディスプレイ ドライバーは、NT ベースのオペレーティング システムを実行している x86 ベースのマシンに全画面表示の MS-DOS アプリケーションの実行時にときどきを除く、エンド ユーザーが表示される表示を制御します。 VGA と互換性のあるミニポート ドライバーでこの機能のサポートに関する詳細については、[VGA と互換性のあるビデオのミニポート ドライバー (Windows 2000 モデル)](vga-compatible-video-miniport-drivers--windows-2000-model-.md)を参照してください。

[ *HwVidInitialize* ](https://msdn.microsoft.com/library/windows/hardware/ff567345)関数を呼び出すことができます[ **VideoPortGetRegistryParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff570316)または[ **VideoPortSetRegistryParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff570365)を取得および構成情報をレジストリに設定します。 たとえば、 *HwVidInitialize*呼び出すことができます**VideoPortSetRegistryParameters**次回のブート レジストリの不揮発性の構成情報を設定します。 呼び出すことがあります**VideoPortGetRegistryParameters**インストール プログラムによってレジストリに書き込む、バス相対、アダプターに固有の構成パラメーターを取得します。

 

 





