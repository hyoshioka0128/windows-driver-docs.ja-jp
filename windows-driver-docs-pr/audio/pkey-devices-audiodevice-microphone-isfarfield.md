---
title: PKEY \_ デバイス \_ audiodevice \_ マイク \_ IsFarField
description: Windows 10 バージョン19H1 以降では、 **PKEY \_ Devices \_ audiodevice \_ マイク \_ IsFarField**プロパティキーを識別します。これは、マイクが遠くのフィールドオーディオをキャプチャするかどうかを示します。
ms.date: 02/13/2019
ms.localizationpriority: medium
ms.openlocfilehash: 585ebeccd3be88e40701d8dcaee6991bc5af8291
ms.sourcegitcommit: 7a69c2e0abf91a57407b13a30faf24925f677970
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85829033"
---
# <a name="pkey_devices_audiodevice_microphone_isfarfield"></a>PKEY \_ デバイス \_ audiodevice \_ マイク \_ IsFarField

Windows 10 19H1 以降では、 **PKEY \_ Devices \_ audiodevice \_ マイク \_ IsFarField**プロパティキーは、マイクが遠くのフィールドオーディオをキャプチャするかどうかを示します。

Windows 10 19H1 以降では、PKEY \_ Devices \_ audiodevice マイク IsFarField プロパティを使用して、 \_ 通常は \_ 音声アシスタントが使用する、遠くのフィールドオーディオをサポートするシステムの要件を示します。

値1は、マイクが遠くのフィールドオーディオをキャプチャすることを示します。これにより、マイクが音声アシスタントの優先エンドポイントになります。

値が0またはプロパティキーがない場合は、マイクが遠くのフィールドをサポートしていないことを示します。または、サポートが不明なため、エンドポイントは音声アシスタントで使用する優先順位が設定されません。

プロパティは、INF を使用して設定する必要があります。また、可能であれば、オーディオデバイスのベース INF ではなく、OEM によって提供される拡張機能 INF を使用します。 拡張機能の INF ファイルの詳細については、「コンポーネント化され[たオーディオドライバーのインストールを作成する](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-universal-drivers#-creating-a-componentized-audio-driver-installation)」および「[拡張機能の Inf ファイルの使用](https://docs.microsoft.com/windows-hardware/drivers/install/using-an-extension-inf-file)」を参照してください。

## <a name="inf-file-sample"></a>INF ファイルのサンプル

Sysvad サンプル ComponentizedAudioSampleExtension ファイルには、このプロパティが含まれています。 このサンプルでは、マイクが遠くのフィールドオーディオをキャプチャすることを示す、0x1 に設定された値を示します。

```inf
;HKR,EP\1,%PKEY_Devices_AudioDevice_Microphone_IsFarField%,0x00010001,0x1
```

## <a name="requirements"></a>必要条件

|要件|値 |
|--- |--- |
|サポートされている最小のクライアント|Windows 10 バージョン19H1|
|Header|Ksmedia.h|

## <a name="related-topics"></a>関連項目

[メディアクラスの INF 拡張機能](media-class-inf-extensions.md)
