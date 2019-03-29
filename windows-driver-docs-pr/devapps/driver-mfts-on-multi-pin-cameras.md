---
title: 複数ピン カメラ ドライバーの仕様を使用します。
description: 一部のカメラは、プレビュー、キャプチャ、および静止画の別々 の pin を指定します。 これらの複数ピン カメラでは、開発者に固有の課題が伴います。 このトピックでは、複数ピン カメラのカメラ driver MFT を開発する際に考慮すべきいくつかの点について説明します。
ms.assetid: E946C676-D1CE-4759-A255-3E16EDCE599F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f811d3e914f270cea15d534a84d4df8673cdefaf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580994"
---
# <a name="span-iddevappsdrivermftsonmulti-pincamerasspanconsiderations-for-driver-mfts-on-multi-pin-cameras-uwp-device-apps"></a><span id="devapps.driver_mfts_on_multi-pin_cameras"></span>複数ピン カメラ (UWP デバイス アプリ) でドライバーの仕様に関する考慮事項


Windows 8.1 は、Ihv および Oem のシステムにも、Media Foundation 変換 (MFT) のカメラ driver MFT と呼ばれる形式でビデオの処理にプラグインを作成する機能を提供します。 インストールされると、これらドライバーの仕様を特別なビデオ特殊効果を有効にする UWP デバイス アプリで使用できます。 一部のカメラは、プレビュー、キャプチャ、および静止画の別々 の pin を指定します。 これらの複数ピン カメラでは、開発者に固有の課題が伴います。 このトピックでは、複数ピン カメラのカメラ driver MFT を開発する際に考慮すべきいくつかの点について説明します。 Driver MFT の作成に関する詳細については、次を参照してください。[カメラ driver MFT 作成](creating-a-camera-driver-mft.md)です。

## <a name="span-idintroductionspanspan-idintroductionspanspan-idintroductionspanintroduction"></a><span id="Introduction"></span><span id="introduction"></span><span id="INTRODUCTION"></span>概要


Driver MFT は、"MFT0 最初 MFT ソース リーダーで動作することを示すために"とも呼ばれます。 MFT0 の個別のインスタンスは、キャプチャ元のすべてのピンにアタッチされます。 いくつかのシステム Oem AVStream キャプチャ ドライバーはプレビュー暗証番号 (pin)、キャプチャの pin、および静止暗証番号 (pin) をサポートする必要があります。 これは、MFT0 の 3 つのインスタンスがあることを意味します。 この図では、このアーキテクチャで、各ストリームに 1 つずつ、IHV プラグイン MFT の 3 つのコピーを示します。

![キャプチャ拡張機能プラグイン モデル mf](images/372842-cameracaptureengine.png)

MFT0 の一般的なシナリオには課題が存在する場合がします。 MFT0 の 2 つの一般的な関数は次のとおりです。

-   (自動公開の前のホスト ベースの自動フォーカスなど) の強化されたキャプチャのカメラにフィードバックを提供するビデオ ストリームを分析

-   ビデオ特殊効果を追加します。

## <a name="span-idone-pinwebcamspanspan-idone-pinwebcamspanspan-idone-pinwebcamspanone-pin-webcam"></a><span id="One-pin_webcam"></span><span id="one-pin_webcam"></span><span id="ONE-PIN_WEBCAM"></span>1-pin の web カメラ


従来は、カメラに公開されて Windows として単一のキャプチャのピン留めします。 この図では、1-pin の web カメラの動作を表します。

![1-pin の web カメラ](images/372826-camera-one-pin-webcam.png)

ここでは、両方のカメラ コントロールおよびビデオの効果は、プレビューおよび静止画のカメラのコントロールとビデオの効果が適用された後に、キャプチャの暗証番号 (pin) から tee 場合があるために設計されたどおりに動作します。 その結果は、保存したファイルまたはユーザーのチャットの友人リストは、プレビューでは、ユーザーに表示される同じビデオ特殊効果で表示されます、カメラ制御機能の 1 つだけのインスタンスが存在します。 アプリが、キャプチャ ピンで MFT0 に接続されている、関連付けられている UWP デバイス アプリがある場合、MFT0 (ユーザー) は、アプリからコントロール メッセージを取得するようにします。

## <a name="span-idthree-pinwebcamspanspan-idthree-pinwebcamspanspan-idthree-pinwebcamspanthree-pin-webcam"></a><span id="Three-pin_webcam"></span><span id="three-pin_webcam"></span><span id="THREE-PIN_WEBCAM"></span>3-pin の web カメラ


3-pin カメラ MFT0、アプリケーションのニーズに応じて最大 3 つのインスタンスがあります。 この図では、3-pin のカメラの動作を表します。

![3-pin の web カメラ](images/372826-camera-three-pin-camera.png)

このような状況は、いくつかの課題を表示します。 最初に、カメラ センサーと ISP の設定を直接制御を必要とするホスト ベースの自動公開ソリューションの場合は、MFT0s の 3 つと同時に、カメラを制御する試行可能性があります。 これには、管理システムが中断されます。

次に、ビデオ特殊効果の可能性のある 3 つのインスタンスがあります。 3 倍の計算コストをかけず、を超えて、MFT0 の 3 つのインスタンスは各ビデオのフレームがまったく同じ状態で同じ効果を常が確実な方法で通信する必要がありますようになりました。 それ以外の場合、ユーザーが認識されません内容が保存または共有します。

さらに、これには 2 つの最終的な複合要素があります。

-   MFT0 の各インスタンスを作成または、いつでもシャット ダウンする可能性があります。

-   UWP デバイスのアプリが、MFT0 の 1 つのインスタンスに接続されているのみ

## <a name="span-idcompressedvideospanspan-idcompressedvideospanspan-idcompressedvideospancompressed-video"></a><span id="Compressed_video"></span><span id="compressed_video"></span><span id="COMPRESSED_VIDEO"></span>圧縮されたビデオ


Web カメラまたはシステムの OEM キャプチャ ピンで提示される前に、ビデオを圧縮することもできます (つまり、自身で web カメラで)。 保存および HD ビデオを共有の下の電源が投入されて Pc を web カメラに圧縮をオフロードできます。 この圧縮ビデオ ストリーム通常分析できませんカメラのコントロールをサポートするためにも、ビデオ特殊効果を適用することができます。 これは、場合は、チャレンジ MFT0 (およびそれが存在する場合、Microsoft Store デバイス アプリ) のすべてのインスタンスのキャプチャのストリームに効果が適用されていないことに注意してください。 この図では、圧縮されたビデオを表します。

![圧縮されたビデオ](images/372826-camera-compressed-video.png)

ユーザーは、プレビュー ストリームにビデオ特殊効果を適用する場合は、キャプチャ ストリームまたは静止暗証番号 (pin) を適用できません。 そのため、ユーザーには、保存またはストリーミングされたビデオに適用されないビデオ特殊効果が表示されます。 プレビュー ストリームが停止した場合、Microsoft Store のデバイス アプリをキャプチャ ストリームへの接続には再試行します。 ユーザーは、圧縮されたビデオをストリーミングは、ときに、多くの機能をこれはできません。

## <a name="span-idcommunicationbetweenmft0instancesspanspan-idcommunicationbetweenmft0instancesspanspan-idcommunicationbetweenmft0instancesspancommunication-between-mft0-instances"></a><span id="Communication_between_MFT0_instances"></span><span id="communication_between_mft0_instances"></span><span id="COMMUNICATION_BETWEEN_MFT0_INSTANCES"></span>MFT0 インスタンス間の通信


MFT0 の 3 つのインスタンスは、互いと通信できる、これと、ほとんどの問題が解決します。 これらのインスタンスが互いを検出する方法は、IHV 責任です。 すべて MFT0s が通信できる、MFT0 のインスタンスは Microsoft Store をデバイス アプリは、どちらの効果が適用されている他のインスタンスをさせることができ、現在の状態に接続します。 また、3 つのインスタンスでは、カメラ コントロールを適用する対象のインスタンスを判断できます。 最後に、プレビューの暗証番号 (pin) は、キャプチャの暗証番号 (pin) がエンコードされたビデオをストリーミングしてかどうかを判断できます。 プレビューの暗証番号 (pin) は、ビデオ特殊効果を無効にできます。

MFT0 のインスタンス間の通信は、主要なユーザー エクスペリエンスの問題を解決するは、ビデオ特殊効果の 3 つのインスタンスが同時に実行されるもする必要があります。 全画面表示のビデオがされているときに特にビデオ効果をいくつかが利用可能なほとんどの CPU リソースを使用できますのプレビューを表示し、同時にキャプチャします。 これらは、深刻な問題です。 パフォーマンス上の理由から、各 ISV はどのような処理が顔の検出など、一度だけ実行し、MFT0 のすべてのインスタンスと共有を検討してください。

 

 





