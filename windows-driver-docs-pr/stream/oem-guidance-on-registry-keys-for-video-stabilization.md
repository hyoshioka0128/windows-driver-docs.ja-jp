---
title: ビデオ手ブレ補正のレジストリ設定
description: VideoStabilization のレジストリ キーに OEM セット MaxPixelsPerSecond 値には、デバイスでビデオ安定化の設定を構成し、キャプチャ時にビデオをビデオ安定化を適用する Oem が有効になります。
ms.assetid: F0F7A705-0F39-4A62-A110-A2E47DFB7B42
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 853b44f4173b322a899e63437be5dc13b655d30f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368099"
---
# <a name="video-stabilization-registry-settings"></a>ビデオ手ブレ補正のレジストリ設定


OEM セット**MaxPixelsPerSecond**値、 **VideoStabilization**レジストリ キーにより、デバイスでビデオ安定化の設定を構成してでビデオをビデオ安定化を適用する Oemキャプチャ時。 構成では、そのハードウェアとソフトウェアの機能と共に、デバイスの記録の解決が考慮されます。

## <a name="overview"></a>概要


**VideoStabilization**レジストリ キー **MaxPixelsPerSecond**最適な状況でのデバイスでビデオ安定化の最大の機能を指定する値を使用します。 すべてのアプリは、レジストリ キーを読み取るし、ビデオ安定化の不合理の使用状況を防ぐ。

入力された値、 **MaxPixelsPerSecond**値は、これを超える MFT しようとしてビデオ安定化、有効にする場合でも、これにより、アプリの制限を設定します。 レジストリ キーは、デバイスがビデオ安定化を実行する最大解像度やフレーム レートを示す必要があります。 場合、 **MaxPixelsPerSecond**値が設定されていないと、ビデオ安定化 MFT はフォールバック値を使用します。 最後に、失敗した場合も、ビデオ安定化はその内部ロジックに最適なユーザー エクスペリエンスを防ぐためにオフに使用します。

## <a name="video-stabilization-requirements"></a>ビデオ安定化の要件


デバイスは、次のすべてのことができますが発生した場合は、ビデオ安定化を実行できると見なされます。

-   ビデオ安定化は有効になり、パススルー モードではないです。

-   記録がオンになっています。

-   プレビューがアクティブ

-   プレビューでノイズまたはフレームのドロップは表示されません。

-   録画済みビデオの音またはフレームのドロップは表示されません。

## <a name="set-the-video-stabilization-registry-key"></a>ビデオ安定化のレジストリ キーを設定します。


**VideoStabilization レジストリ キーの形式:**

-   Oem を設定する必要があります、 **MaxPixelsPerSecond**アプリで有効になっている場合でも、パススルーのモードで実行するどのビデオ安定化を強制は、2 つ目以外にもあたりのピクセルの数のカットオフ値を定義する QWORD 値。

-   **MaxPixelsPerSecond**が次のように定義されています。

    `MaxPixelsPerSecond = width * height * frame-rate`

    たとえば、30 fps で 1080p の解像度**MaxPixelsPerSecond**が 1920年として定義されます\*1080 \* 30 = 62208000 します。

**VideoStabilization レジストリ キーの場所:**

-   Oem が作成および設定する必要があります、 **VideoStabilization**次の場所にビデオ安定化のレジストリ キー。

    **HKEY\_ローカル\_マシン\\ソフトウェア\\Microsoft\\Windows メディア ファンデーション\\プラットフォーム\\VideoStabilization**

    設定する、 **VideoStabilization**レジストリ キー **MaxPixelsPerSecond**値の 32 ビット コンピューターで、管理者特権のコマンド プロンプトで次のコマンドを使用します。

    ```console
    reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Media Foundation\Platform\VideoStabilization" /v "MaxPixelsPerSecond" /t REG_QWORD /d 62208000 /f 
    ```

-   64 ビット コンピューターで、Oem も作成し、Wow6432Node パスに同じキーを設定する必要があります。

    **HKEY\_ローカル\_マシン\\ソフトウェア\\Wow6432Node\\Microsoft\\Windows メディア ファンデーション\\プラットフォーム\\VideoStabilization**

    設定する、 **VideoStabilization**レジストリ キー **MaxPixelsPerSecond**値の 64 ビット コンピューターで、管理者特権のコマンド プロンプトで次のコマンドを使用します。

    ```console
    reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Windows Media Foundation\Platform\VideoStabilization" /v "MaxPixelsPerSecond" /t REG_QWORD /d 62208000 /f 
    ```

これを設定すると、 **VideoStabilization**レジストリ キーは、ビデオ安定化 MFT と 1 つ目とサード パーティ製アプリに表示されます。

場合、 **MaxPixelsPerSecond**値が設定 MFT は、フレーム レートや制限を超えての解像度を安定化することはありません試みますビデオ安定化します。 代わりに、アプリ ビデオ安定化を要求する場合でも、パススルー モードに切り替わりますがされます。 ビデオ安定化 MFT フレーム レートと解像度を特定のデバイスのアプリに推奨するメカニズムを持っていません。 アプリでは、レジストリ キーが設定されますが、それらのデバイスで、このようなパススルーを回避するために推奨事項を選択できます。

場合、 **MaxPixelsPerSecond**値が設定されていない MFT は既定値になるまで、それを超えないを安定化しようとします。 ビデオ安定化します。

既定値は、1920年ピクセル x 1080 ピクセル x 30 fps は、1 秒あたりの 62208000 ピクセルです。 ビデオ安定化では、安定した状態にしようとしていますが、ビデオのフレームのリアルタイムの安定化を維持することはできません、内部ロジックはビデオ安定化をすべてのフレームを削除せず (ビデオ安定化をオフにする) パススルー モードに切り替えます。

ビデオ安定化前のセッションでオフになって、MFT はパススルー モードに切り替えるに決定する前に、すべての新しいセッションの通常モードでビデオ安定化を開始しようとします。 これは、ことに依存することが最後に運用されるときに、ストレス条件下で、デバイスをされているため、将来決定を行うには、前のモードであるためにです。

## <a name="video-stabilization-test-requirements"></a>ビデオ安定化のテスト要件


Oem は、ビデオ安定化作業に自分のデバイスのエンド ツー エンド機能を確認する必要があります。 特定の最大ピクセルあたり 2 つ目の解決に許容可能な経験をことを確認する必要があります。

Oem は、次のことを確認する必要があります。

-   Microsoft によって提供されるレジストリ キーの場所では、ビデオ安定化の内部ロジックが無効です。 内部ロジックを無効にするビデオ安定化がストレスの多い状況が発生した場合のテスト中のパススルー モードに移動されることを保証します。

-   ビデオ安定化はバック グラウンド タスクまたはその他の機能せず、単独で実行できます。

-   有効になっているビデオ安定化と無効になっている内部ロジックを使用した smooth プレビューのレンダリング

-   スムーズにビデオ記録を有効になっているビデオ安定化と無効になっている内部ロジック

-   目的のピクセルあたり 2 つ目の数が安定した録画で実現

-   過熱なし

**注**小売システムには、このセクションで説明するビデオ安定化の内部ロジックを無効にするレジストリ キーはありません。 ただし、小売システムが必要、 **VideoStabilization**レジストリ キーを**MaxPixelsPerSecond**値がこのテスト プロセスを使用して決定します。


**注**、 **VideoStabilization**レジストリ キー **MaxPixelsPerSecond**値関数だけとき属性[MF\_低\_待機時間](https://docs.microsoft.com/windows/desktop/medfound/mf-low-latency)で効果に設定されます。 MediaCapture パイプラインに指定されたビデオ安定化の効果を追加すると、属性が自動的に設定します。 ただし、ビデオ安定化の効果がカスタム パイプラインをまたはに設定されないパイプラインに挿入された場合、 **MF\_低\_待機時間**属性、レジストリ キーが影響を与えません。
