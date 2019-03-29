---
title: 鍵\_デバイス\_AudioDevice\_マイク\_IsFarField
description: Windows 10 バージョン 19 H で 1 以降、**鍵\_デバイス\_AudioDevice\_マイク\_IsFarField**プロパティのキーを識別、マイクが遠くのフィールドをキャプチャすることを示しますオーディオです。
ms.date: 02/13/2019
ms.localizationpriority: medium
ms.openlocfilehash: 89a38c5cd59318c13d9c1e7ce248bad62eb1138f
ms.sourcegitcommit: 5f4404a7010a6b26530f60144c5ea7cab846feec
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2019
ms.locfileid: "56582953"
---
# <a name="pkeydevicesaudiodevicemicrophoneisfarfield"></a>鍵\_デバイス\_AudioDevice\_マイク\_IsFarField

Windows 10 で 19 H 1 以降、**鍵\_デバイス\_AudioDevice\_マイク\_IsFarField**プロパティのキーは、フィールドのオーディオ、マイクははるかにキャプチャされてかどうかを示します。 

Windows 10 以降 19 H 1、鍵を使用して\_デバイス\_AudioDevice\_マイク\_までをサポートするシステム フィールドの音声アシスタントによって使用される通常のオーディオの IsFarField プロパティが必要です。 

値 1 は、マイクがまでフィールド オーディオ、するには、マイクに適したエンドポイントの音声アシスタントでキャプチャはことを示します。 

値 0 またはプロパティ キーがないのでは、音声アシスタントを使用するため、エンドポイントが優先しないが、マイクが相手側のフィールドをサポートしていないか、サポートが、不明なことを示します。

プロパティは、INF、および可能であればオーディオ デバイスの基本の INF ではなく、OEM によって提供される、拡張子 INF を使用して設定する必要があります。 拡張子 INF ファイルの詳細については、次を参照してください。[コンポーネント化されたオーディオ ドライバーのインストールを作成する](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-universal-drivers#-creating-a-componentized-audio-driver-installation)と[拡張子 INF ファイルを使用して](https://docs.microsoft.com/windows-hardware/drivers/install/using-an-extension-inf-file)します。




## <a name="span-idinffilesamplespanspan-idinffilesamplespanspan-idinffilesamplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>サンプルの INF ファイル

Sysvad サンプル ComponentizedAudioSampleExtension.inf ファイルには、このプロパティが含まれています。 このサンプルでは、マイクがはるかに音声をフィールドでキャプチャを示す 0x1 に設定された値を示します。

```inf
;HKR,EP\1,%PKEY_Devices_AudioDevice_Microphone_IsFarField%,0x00010001,0x1
```

<a name="requirements"></a>必要条件
------------

|||
|--- |--- |
|サポートされている最小のクライアント|Windows 10 のバージョン 1 の 19 H|
|Header|Ksmedia.h|

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

[Media クラス INF の拡張機能](media-class-inf-extensions.md)

 

 






