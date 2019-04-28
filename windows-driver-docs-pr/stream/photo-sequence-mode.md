---
title: 写真シーケンス モード
description: フォト シーケンス モードでは、カメラの写真を 1 つクリックに応答の写真のシーケンスをキャプチャできます。
ms.assetid: 15F19FE1-6D09-4406-B096-E96D12BAF030
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c16d3e37211956e9b5d93bcaa2056b849738f1fe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362362"
---
# <a name="photo-sequence-mode"></a>写真シーケンス モード


フォト シーケンス モードでは、カメラの写真を 1 つクリックに応答の写真のシーケンスをキャプチャできます。 このモードでキャプチャのシステムは、シーケンス内の写真をキャプチャするカメラ ドライバーにバッファーを継続的に送信します。 このモードでは、写真をクリックする前に期間から写真をキャプチャできます。

## <a name="photo-sequence-operation"></a>写真のシーケンスの操作


カメラのドライバーをサポートしています、 [ **KSPROPERTY\_CAMERACONTROL\_拡張\_PHOTOMODE** ](https://msdn.microsoft.com/library/windows/hardware/dn567582)場合は、制御が写真をシーケンス処理できます。 キャプチャ パイプライン送信することによって、写真のシーケンスを開始する、 **KS\_VideoControlFlag\_StartPhotoSequenceCapture**フォト ストリームをトリガーします。 この時点では、ドライバーでは、キャプチャ バッファーの送信を開始する必要があります。 キャプチャのパイプライン送信することによって、写真のシーケンスを停止**KS\_VideoControlFlag\_StopPhotoSequenceCapture**フォト ストリームをトリガーします。 完了した各写真の新しいバッファーは、ドライバーにフレームをキャプチャするためにに送信されます。

キャプチャ パイプラインでは、特定のフォト シーケンス セッションのために必要な過去のフレームの数によって構成されますフォト シーケンス モードの構成フェーズがあります。 構成フェーズでは、ドライバーには、過去のフォト フレームの最大数を指定する必要があります。 また、ドライバーでは、必要な過去のフレーム数をサポートするために必要なバッファー数を指定します。

拡張コントロール、 [ **KSPROPERTY\_CAMERACONTROL\_拡張\_PHOTOTRIGGERTIME**](https://msdn.microsoft.com/library/windows/hardware/dn567584)は、ユーザーが写真のトリガーをクリックした実際の時間を渡します写真のシーケンスを実行するカメラ アプリケーション。 この時刻のないドライバーが登録されていないときにフレームを返すを開始するキャプチャどの写真、 **KS\_VideoControlFlag\_StartPhotoSequenceCapture**トリガーが到着します。 このコントロールでは、指定された写真のトリガーの時刻に最も近い写真を返す、ドライバーが必要です。

## <a name="frame-count-negotiation"></a>フレームの数のネゴシエーション


次の一連の操作は、カメラのドライバーの写真のモードとフレームの数を設定します。

1.  アプリケーションでは、写真のシーケンスのキャプチャのキャプチャのシステムとドライバーを準備するための API を呼び出します。

2.  キャプチャのシステムは、ドライバーに、呼び出しに写真モード拡張プロパティ要求を送信[ **KSPROPERTY\_CAMERACONTROL\_拡張\_PHOTOMODE** ](https://msdn.microsoft.com/library/windows/hardware/dn567582)でKSCAMERA\_EXTENDEDPROP\_PHOTOMODE\_シーケンス写真シーケンス モードのドライバーの移行を開始するフラグを設定します。

    1.  ドライバーには、アプリケーションから要求された履歴のフレーム数が与えられます。 ドライバーは、履歴のフレームを保持するために必要なバッファーの数と共にサポートすることは履歴のフレーム数を返す必要があります。

    2.  ドライバーは、フォト シーケンス モードの遷移の呼び出しを使用してバッファーの数と、暗証番号 (pin) のアロケーターの要件の構造を更新する必要があります**KsEdit**します。

    3.  ドライバーは、内部状態を写真シーケンス モードに変更されます。

3.  キャプチャ システム遷移 KSSTATE にピン留め\_を実行し、写真シーケンス モードに対して要求されたバッファーの数と、ドライバーを提供します。

## <a name="control-support-requirements"></a>コントロールのサポート要件


次のコントロールの拡張のサポートは、写真シーケンス モードをサポートするためにカメラのドライバーに必要です。

-   写真のモード

    管理: [**KSPROPERTY\_CAMERACONTROL\_拡張\_PHOTOMODE**](https://msdn.microsoft.com/library/windows/hardware/dn567582)

-   フォト フレーム レート

    管理: [**KSPROPERTY\_CAMERACONTROL\_拡張\_PHOTOFRAMERATE**](https://msdn.microsoft.com/library/windows/hardware/dn567580)

-   最大フレーム レートの写真

    管理: [**KSPROPERTY\_CAMERACONTROL\_拡張\_PHOTOMAXFRAMERATE**](https://msdn.microsoft.com/library/windows/hardware/dn567581)

-   トリガー時間の写真

    管理: [**KSPROPERTY\_CAMERACONTROL\_拡張\_PHOTOTRIGGERTIME**](https://msdn.microsoft.com/library/windows/hardware/dn567584)

-   サムネイルの写真

    管理: [**KSPROPERTY\_CAMERACONTROL\_拡張\_PHOTOTHUMBNAIL**](https://msdn.microsoft.com/library/windows/hardware/dn567583)

-   最大ビデオ フレーム レート

    管理: [**KSPROPERTY\_CAMERACONTROL\_拡張\_MAXVIDFPS\_PHOTORES**](https://msdn.microsoft.com/library/windows/hardware/dn567578)

-   フラッシュのモード (KSCAMERA をサポートしている\_EXTENDEDPROP\_FLASH\_SINGLEFLASH 機能)

    管理: [**KSPROPERTY\_CAMERACONTROL\_拡張\_FLASHMODE**](https://msdn.microsoft.com/library/windows/hardware/dn567575)

 

 




