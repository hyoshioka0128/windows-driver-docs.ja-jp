---
title: ソフトウェア音量制御のサポート
description: ソフトウェア音量制御のサポート
ms.assetid: 2bdc7d01-9e47-4deb-b551-13e9cbc9c844
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25d2fad43f553c9168788ba98341b8fad7389573
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328646"
---
# <a name="software-volume-control-support"></a>ソフトウェア音量制御のサポート


Windows Vista 以降では、オーディオ ハードウェアが含まれていないと、関連付けられている物理ボリューム コントロールとアンプのソフトウェアのボリュームのサポートが提供されます。

次の図は、Windows ソフトウェアのボリュームのサポートの簡略化された表現を示します。

![windows vista のソフトウェアのボリュームを示す図をサポートします。 ](images/audio-volume-architecture.png)

図には、2 つの個別のオーディオ データ パスを示します。 1 つと Windows APO ソフトウェアのボリューム コントロールを使用するとアンプが存在し、1 つです。 アンプが存在する場合、ドライバーがアドバタイズ KSPROPERTY\_オーディオ\_VOLUMELEVEL します。 かどうか、オーディオ ドライバーは示しません KSPROPERTY をサポートしている\_オーディオ\_VOLUMELEVEL、Windows オーディオ エンジンは、APO ソフトウェア ボリューム コントロールを作成します。

一般的な pc では、これらのデータ パスの 1 つだけ表示されます、一般的になるので、コンピューターのオーディオのコンポーネントの 1 つのセット。 2 つのパスは、例示を目的としてここに表示されます。

[ **IAudioEndpointVolume** ](https://msdn.microsoft.com/library/windows/desktop/dd370892)またはオーディオ エンドポイント デバイスから、インターフェイスがオーディオ ストリーム上のボリューム コントロールを表します。

Bluetooth または USB オーディオが存在する場合、ボリューム コントロールを個別に制御されます。

## <a name="span-iddatapathwithamplifierpresentspanspan-iddatapathwithamplifierpresentspanspan-iddatapathwithamplifierpresentspandata-path-with-amplifier-present"></a><span id="Data_path_with_amplifier_present"></span><span id="data_path_with_amplifier_present"></span><span id="DATA_PATH_WITH_AMPLIFIER_PRESENT"></span>アンプ存在でのデータ パス


クライアント アプリケーションを呼び出すと、 [ **IAudioEndpointVolume** ](https://msdn.microsoft.com/library/windows/desktop/dd370892)アンプがあるし、物理ボリューム コントロール、オーディオ ドライバー KSNODETYPEを公開する場所の構成でインターフェイス\_トポロジのフィルターで [ボリューム] ノード。 [ボリューム] ノードの存在により、 **IAudioEndpointVolume**ハードウェアでオーディオ信号のボリューム レベルを変更することに注意してください。

## <a name="span-iddatapathwithnoamplifierpresentspanspan-iddatapathwithnoamplifierpresentspanspan-iddatapathwithnoamplifierpresentspandata-path-with-no-amplifier-present"></a><span id="Data_path_with_no_amplifier_present"></span><span id="data_path_with_no_amplifier_present"></span><span id="DATA_PATH_WITH_NO_AMPLIFIER_PRESENT"></span>存在しないアンプでのデータ パス


アンプが存在するがない場合に[ **IAudioEndpointVolume** ](https://msdn.microsoft.com/library/windows/desktop/dd370892) APO をサポートする Windows ソフトウェアのボリュームを初期化するために、オーディオ エンジンで動作します。

モデル化する物理ボリューム コントロールがないため、KSNODETYPE\_トポロジ フィルターで [ボリューム] ノードは公開されません。 ボリュームの減衰と向上は、APO ソフトウェアのボリュームのサポート コンポーネントによって実行されます。

ボリュームの範囲と異なるバージョンの Windows の既定のボリューム レベルについては、次を参照してください。[既定のオーディオ音量設定](default-audio-volume-settings.md)します。

 

 




