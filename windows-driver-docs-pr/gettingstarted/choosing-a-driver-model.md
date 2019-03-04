---
title: ドライバー モデルの選択
description: Microsoft Windows には、ドライバーの作成に使うことができる、さまざまなドライバー モデルが用意されています。
ms.assetid: 67de6453-969e-4b4d-a72e-de132b20b022
keywords:
- ドライバー モデル
- ドライバー設計
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 509f523f2e7829d0b806eee122390db396b2988b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518853"
---
# <a name="choosing-a-driver-model"></a>ドライバー モデルの選択


Microsoft Windows には、ドライバーの作成に使うことができる、さまざまなドライバー モデルが用意されています。 最適なドライバー モデルを選ぶための戦略は、作成を予定しているドライバーの種類によって異なります。 次のオプションがあります。

-   デバイス ファンクション ドライバー
-   デバイス フィルター ドライバー
-   ソフトウェア ドライバー
-   ファイル システム フィルター ドライバー
-   ファイル システム ドライバー

さまざまな種類のドライバーの違いについては、「[ドライバーとは](what-is-a-driver-.md)」と「[デバイス ノードとデバイス スタック](device-nodes-and-device-stacks.md)」をご覧ください。 次のセクションでは、ドライバーの種類ごとにモデルの選択方法について説明します。

## <a name="span-idchoosingadrivermodelforadevicefunctiondriverspanspan-idchoosingadrivermodelforadevicefunctiondriverspanchoosing-a-driver-model-for-a-device-function-driver"></a><span id="choosing_a_driver_model_for_a_device_function_driver"></span><span id="CHOOSING_A_DRIVER_MODEL_FOR_A_DEVICE_FUNCTION_DRIVER"></span>デバイス ファンクション ドライバーのドライバー モデルの選択


ハードウェア デバイスを設計するときには、ファンクション ドライバーを作る必要があるかどうかをまず検討する必要があります。 以下の点を確認してください。

ドライバー全部を作ることを避けられるか。
ファンクション ドライバーを作る必要がある場合、使うべき最適なドライバー モデルはどれか。
これらを確認するために、「[デバイスとドライバーのテクノロジ](https://docs.microsoft.com/windows-hardware/drivers/device-and-driver-technologies)」に説明されているテクノロジの一覧でデバイスが適合する箇所を特定します。 特定したテクノロジのドキュメントを参照して、ファンクション ドライバーを作る必要があるかどうかを判断し、デバイスに使用可能なドライバー モデルについて確認します。

個々のテクノロジの中には、ミニドライバー モデルがあるものもあります。 ミニドライバー モデルでは、デバイス ドライバーは、汎用的なタスクを処理する部分とデバイス固有のタスクを処理する部分の 2 つの部分で構成されます。 一般に、Microsoft が汎用的な部分を作成し、デバイスの製造元がデバイス固有の部分を作成します。 デバイス固有の部分にはさまざまな名前が付けられますが、ほとんどはプレフィックス *mini* を共有しています。 ミニドライバー モデルで使われる名前をいくつか示します。

-   ディスプレイ ミニポート ドライバー
-   オーディオ ミニポート ドライバー
-   バッテリ ミニクラス ドライバー
-   Bluetooth プロトコル ドライバー
-   HID ミニドライバー
-   WIA ミニドライバー
-   NDIS ミニポート ドライバー
-   ストレージ ミニポート ドライバー
-   ストリーミング ミニドライバー

ミニドライバー モデルの概要については、「[ミニドライバーとドライバーのペア](minidrivers-and-driver-pairs.md)」をご覧ください。

「[デバイスとドライバーのテクノロジ](https://docs.microsoft.com/windows-hardware/drivers/device-and-driver-technologies)」に一覧表示されているテクノロジのすべてに、専用のミニドライバー モデルがあるわけではありません。 ある特定のテクノロジのドキュメントでは[カーネル モード ドライバー フレームワーク (KMDF)](https://docs.microsoft.com/windows-hardware/drivers/wdf/) を、他のテクノロジのドキュメントでは[ユーザー モード ドライバー フレームワーク (UMDF)](https://docs.microsoft.com/windows-hardware/drivers/wdf/) を使うよう勧められていることがあります。 重要なのは、特定のデバイス テクノロジのドキュメントを研究することから始める必要があるという点です。 デバイス テクノロジにミニドライバー モデルがある場合、そのミニドライバー モデルを使う必要があります。 それ以外の場合は、UMDF、KMDF、Windows Driver Model (WDM) のどれを使うかについて、テクノロジ固有のドキュメントの助言に従います。

## <a name="span-idchoosingadrivermodelforadevicefilterdriverspanspan-idchoosingadrivermodelforadevicefilterdriverspanspan-idchoosingadrivermodelforadevicefilterdriverspanchoosing-a-driver-model-for-a-device-filter-driver"></a><span id="Choosing_a_driver_model_for_a_device_filter_driver"></span><span id="choosing_a_driver_model_for_a_device_filter_driver"></span><span id="CHOOSING_A_DRIVER_MODEL_FOR_A_DEVICE_FILTER_DRIVER"></span>デバイス フィルター ドライバーのドライバー モデルの選択


デバイスからのデータ読み取りのような単一の I/O 要求に複数のドライバーが関与していることがよくあります。 ドライバーは 1 つのスタック上に重ねて置かれます。スタックの状態を視覚的に捉えるために、最初のドライバーが最上部に、最後のドライバーが最下部にそれぞれ置かれているイメージにたとえる方法がよく用いられます。 スタックには 1 つのファンクション ドライバーがあり、フィルター ドライバーを置くこともできます。 ファンクション ドライバーとフィルター ドライバーについては、「[ドライバーとは](what-is-a-driver-.md)」と「[デバイス ノードとデバイス スタック](device-nodes-and-device-stacks.md)」をご覧ください。

デバイスのフィルター ドライバーを作る準備をしている場合、「[デバイスとドライバーのテクノロジ](https://docs.microsoft.com/windows-hardware/drivers/device-and-driver-technologies)」に説明されているテクノロジの一覧で、デバイスが適合する箇所を特定します。 特定したテクノロジのドキュメントに、フィルター ドライバー モデルの選択に関するガイダンスがあるかどうかを確認します。 デバイス テクノロジのドキュメントにガイダンスがない場合は、まず UMDF をドライバー モデルとして使うことを検討します。 フィルター ドライバーが、UMDF からは利用できないデータ構造にアクセスする必要がある場合は、KMDF をドライバー モデルとして使うことを検討します。 非常にまれなケースですが、ドライバーが KMDF からは利用できないデータ構造にアクセスする必要がある場合は、WDM をドライバー モデルとして使います。

## <a name="span-idchoosingadrivermodelforasoftwaredriverspanspan-idchoosingadrivermodelforasoftwaredriverspanspan-idchoosingadrivermodelforasoftwaredriverspanchoosing-a-driver-model-for-a-software-driver"></a><span id="Choosing_a_driver_model_for_a_software_driver"></span><span id="choosing_a_driver_model_for_a_software_driver"></span><span id="CHOOSING_A_DRIVER_MODEL_FOR_A_SOFTWARE_DRIVER"></span>ソフトウェア ドライバーのドライバー モデルの選択


デバイスに関連付けられていないドライバーは、*ソフトウェア ドライバー*と呼ばれます。 ソフトウェア ドライバーついては、「[ドライバーとは](what-is-a-driver-.md)」をご覧ください。 ソフトウェア ドライバーは、カーネル モードで実行可能であり、そのため保護されたオペレーティング システム データにアクセスできるので便利です。 プロセッサ モードについては、「[ユーザー モードとカーネル モード](user-mode-and-kernel-mode.md)」をご覧ください。

ソフトウェア ドライバーでは、2 つのオプションは KMDF と kernel-modeWindows NT ドライバー モデルです。 KMDF と kernel-modeWindows NT ドライバー モデルでは、プラグ アンド プレイ (PnP) や電源管理を心配せずにドライバーを作ることができます。 したがって、ドライバーの主要タスクに集中することができます。 KMDF では、フレームワークによって PnP と電源が処理されるため、PnP や電源について心配する必要はありません。 kernel-modeWindows NT モデルでは、kernel-mode サービスは PnP や電源管理とは完全に独立した環境で動作するため、PnP や電源について心配する必要はありません。

KMDF を使い慣れている場合は特に、KMDF を使うことをお勧めします。 ドライバーを PnP と電源管理から完全に独立したものにするには、kernel-modeWindows NT モデルを使ってください。 電源切り替えまたは PnP イベントを認識するソフトウェア ドライバーを作る必要がある場合、kernel-modeWindows NT モデルは使うことができません。KMDF を使う必要があります。

**注**  非常にまれなケースですが、PnP または電源イベントを認識するソフトウェア ドライバーを作る必要があり、ドライバーが KMDF からは利用できないデータにアクセスする必要がある場合は、WDM を使う必要があります。

## <a name="span-idchoosingadrivermodelforafilesystemdriverspanspan-idchoosingadrivermodelforafilesystemdriverspanspan-idchoosingadrivermodelforafilesystemdriverspanchoosing-a-driver-model-for-a-file-system-driver"></a><span id="Choosing_a_driver_model_for_a_file_system_driver"></span><span id="choosing_a_driver_model_for_a_file_system_driver"></span><span id="CHOOSING_A_DRIVER_MODEL_FOR_A_FILE_SYSTEM_DRIVER"></span>ファイル システム ドライバーのドライバー モデルの選択


ファイル システム フィルター ドライバーのモデルの選択については、「[File system driver samples](https://docs.microsoft.com/windows-hardware/drivers/samples/file-system-driver-samples)」(ファイル システム ドライバーのサンプル) をご覧ください。 ファイル システム ドライバーは非常に複雑になる場合があり、ドライバー開発の高度な概念に関する知識が必要になることがあります。


## <a name="span-idchoosingadrivermodelforafilesystemfilterdriverspanspan-idchoosingadrivermodelforafilesystemfilterdriverspanspan-idchoosingadrivermodelforafilesystemfilterdriverspanchoosing-a-driver-model-for-a-file-system-filter-driver"></a><span id="Choosing_a_driver_model_for_a_file_system_filter_driver"></span><span id="choosing_a_driver_model_for_a_file_system_filter_driver"></span><span id="CHOOSING_A_DRIVER_MODEL_FOR_A_FILE_SYSTEM_FILTER_DRIVER"></span>ファイル システム フィルター ドライバーのドライバー モデルの選択


ファイル システム フィルター ドライバーのモデルの選択については、「ファイル システム ミニフィルター ドライバー」と「[File system filter drivers](https://msdn.microsoft.com/library/windows/hardware/ff540382)」(ファイル システム フィルター ドライバー) をご覧ください。

## <a name="span-idchoosingadrivermodelforafilesystemminifilterdriverspanspan-idchoosingadrivermodelforafilesystemminifilterdriverspanspan-idchoosingadrivermodelforafilesystemminifilterdriverspanchoosing-a-driver-model-for-a-file-system-minifilter-driver"></a><span id="Choosing_a_driver_model_for_a_file_system_minifilter_driver"></span><span id="choosing_a_driver_model_for_a_file_system_minifilter_driver"></span><span id="CHOOSING_A_DRIVER_MODEL_FOR_A_FILE_SYSTEM_MINIFILTER_DRIVER"></span>ファイル システム ミニフィルター ドライバーのドライバー モデルの選択


ファイル システム ミニフィルター ドライバーのモデルの選択については、「[File System Minifilter Drivers](https://msdn.microsoft.com/library/windows/hardware/ff540402)」(ファイル システム ミニフィルター ドライバー) をご覧ください。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[カーネル モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)

[ユーザー モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)

 

 






