---
title: 鍵\_APO\_SWFallback\_ProcessingModes
description: Windows 10 バージョン 1709 以降、鍵で\_APO\_SWFallback\_ProcessingModes プロパティのキーは、処理モードのドライバーでサポートされているソフトウェアにフォールバックできます HW モードを識別します。
ms.date: 10/22/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: f1ca0b1026dba18f52644d62385fb7ac09dacf81
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578600"
---
# <a name="pkeyaposwfallbackprocessingmodes"></a>鍵\_APO\_SWFallback\_ProcessingModes

Windows 10 バージョンは 1809、以降、*鍵\_APO\_SWFallback\_ProcessingModes*プロパティのキーは、フォールバックしてソフトウェアの処理モードを識別します。 ドライバー開発者向けでは、サポート ソフトウェア フォールバック、ドライバーがサポートするモードの処理モードの効果のすべてリストします。 この一覧は、ハードウェアのドライバーがサポートするすべてのモードを網羅する必要があります。

ストリームがこれらのモードのいずれかの要求しその処理モードでは、暗証番号 (pin) を開くには使用可能なハードウェア リソースが不足のため、pin は RAW モードで表示および要求の処理モードを使用して初期化 SW APO が使用されます。 このため、処理モードでは、ハードウェアのソフトウェア フォールバックをサポートするドライバーは、RAW モードをサポートする必要があります。 オーディオ モードの詳細については、[オーディオ信号の処理モード](audio-signal-processing-modes.md)を参照してください。 ソフトウェアのフォールバックは、ホストの暗証番号 (pin) にのみ適用されます。

ストリームが作成され、ハードウェアで使用可能なリソースがない場合は、SW のフォールバックがトリガーされます。 OS では、ドライバー ソフトウェア フォールバックが必要なかどうかを判断する利用可能なリソースを直接クエリします。 OS では、暗証番号 (pin) インスタンスの数が、ドライバーによってサポートされているなど、ドライバーのナレッジを使用して、十分なハードウェア リソースがないか判断します。  ハードウェア リソースが利用できない場合は、ソフトウェア フォールバックが生の暗証番号 (pin) のストリームを作成に使用されます。 ソフトウェア フォールバック プロセスは、OS によって管理され、ソフトウェア フォールバックが発生した場合、ドライバーからの入力は不要です。 ドライバーは、SWFallback を使用する追加の特定のエラー コードを返す必要はありません。

オーディオの制約が指定されている場合、OS はそれらを比較する追加のチェックを行います。 詳細については、[オーディオ ハードウェア リソースの管理](audio-hardware-resource-management.md)を参照してください。

ドライバーは、その FxPropertyStore でサポートされているフォールバック モードがある必要があります。 任意の AUDIO_SIGNALPROCESSINGMODEs SWFallback は、13 PKEY_APO_SWFallback_ProcessingModes {D3993A3F-99C2-4402-B5EC-A92A0367664B} には、ドライバーの FxPropertyStore に追加する必要があります。 これにより、SWFallback の認識にできます。 



###  <a name="pkeyaposwfallbackprocessingmodes-definition"></a>鍵\_APO\_SWFallback\_ProcessingModes 定義

*鍵\_APO\_SWFallback\_ProcessingModes*次に示すように定義されます。

```inf
PKEY_APO_SWFallback_ProcessingModes (REG_MULTI_SZ) = {D3993A3F-99C2-4402-B5EC-A92A0367664B},13 
```


### <a name="span-idinffilesamplespanspan-idinffilesamplespanspan-idinffilesamplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>サンプルの INF ファイル

INF ファイルのプロパティのキーには、ホスト コネクタでサポートされるのに十分なハードウェア リソースが使用できない場合は、SW APO へのフォールバックの使用できるシグナル処理モードが一覧表示します。 

INF ファイルでは、そのデバイスの追加レジストリ セクションの設定を指定します。 文字列とレジストリの追加のセクションでは、APO ソフトウェア フォールバック処理モードをレジストリにロードする INF の次の例を示しています。 この例では 4 つのモードは実装されている、生の既定で、ムービーと通信します。 

```cpp
[Strings]
PKEY_APO_SWFallback_ProcessingModes  = "{D3993A3F-99C2-4402-B5EC-A92A0367664B},13"
...
AUDIO_SIGNALPROCESSINGMODE_DEFAULT = "{C18E2F7E-933D-4965-B7D1-1EEF228D2AF3}"
AUDIO_SIGNALPROCESSINGMODE_MOVIE   = "{B26FEB0D-EC94-477C-9494-D1AB8E753F6E}"
AUDIO_SIGNALPROCESSINGMODE_COMMUNICATIONS = "{98951333-B9CD-48B1-A0A3-FF40682D73F7}"
...
[PKEY.APO.SWFallback.AddReg]
;Include all supported modes:
HKR,"FX\\0",%PKEY_APO_SWFallback_ProcessingModes%,%REG_MULTI_SZ%,%AUDIO_SIGNALPROCESSINGMODE_DEFAULT%,%AUDIO_SIGNALPROCESSINGMODE_MOVIE%,%AUDIO_SIGNALPROCESSINGMODE_COMMUNICATIONS%
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Media クラス INF の拡張機能](media-class-inf-extensions.md)

 

 

[このトピックに関するご感想を Microsoft までお寄せください](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[audio/audio]:%20PKEY_MFX_ProcessingModes_Supported_For_Streaming%20%20RELEASE:%20%2811/22/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20 https://privacy.microsoft.com/default.aspx. "このトピックに関するご感想を Microsoft までお寄せください")





