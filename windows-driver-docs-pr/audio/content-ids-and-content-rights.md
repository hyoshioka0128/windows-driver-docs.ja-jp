---
title: コンテンツ ID とコンテンツの権利
description: コンテンツ ID とコンテンツの権利
ms.assetid: aee123e4-bc1b-4ba8-9f8d-a9d207297c8d
keywords:
- WDK オーディオのコンテンツの権限
- コンテンツ Id WDK オーディオ
- Rights Management の WDK のデジタル オーディオ、コンテンツ Id
- DRM WDK オーディオ、コンテンツ Id
- デジタル権利管理の WDK のオーディオ、コンテンツの権限
- DRM WDK のオーディオ、コンテンツの権限
- 識別子の WDK オーディオ
- 混合ストリーム WDK オーディオ
- DigitalOutputDisable フラグ
- CopyProtect フラグ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c87c077220de72741cb932713ddcffa4abf4ee6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333880"
---
# <a name="content-ids-and-content-rights"></a>コンテンツ ID とコンテンツの権利


## <span id="content_ids_and_content_rights"></span><span id="CONTENT_IDS_AND_CONTENT_RIGHTS"></span>


コンテンツ ID (識別子) は、ULONG 値、 [DRMK システム ドライバー](kernel-mode-wdm-audio-components.md#drmk_system_driver)フィードを特定の pin にオーディオ データ ストリームの DRM で保護されたコンテンツを識別するために実行時に生成されます。

コンテンツの権限は、デジタルの再生または DRM で保護されたコンテンツをコピーするコンテンツ プロバイダーによってユーザーに付与された権限の表現です。 権限がの形式で指定されたコンテンツを[ **DRMRIGHTS** ](https://msdn.microsoft.com/library/windows/hardware/ff536355) DRMK はオーディオ ドライバーに渡される構造体。

DRMRIGHTS には、2 つのフラグが含まれています。**DigitalOutputDisable**と**CopyProtect**します。 場合、 **DigitalOutputDisable**フラグが設定されて、ドライバーには、外部のデバイスに接続するすべてのデジタル出力が無効にする必要があります (たとえばの S/PDIF コネクタ) を経由します。 場合、 **CopyProtect**フラグが設定されて、ドライバーはディスクやその他の形式の不揮発性ストレージに保存するセキュリティで保護されたコンテンツの永続的なコピーを許可する場合があります機能を無効にする必要があります。 たとえば、典型的なオーディオ ハードウェアは、キャプチャ チャネルを介してルーティングされるようにする再生信号を使用できます。 この信号がデジタル形式である場合は、キャプチャされた信号には入力信号の完璧なデジタル コピー可能性があります。 再生、ミックスを持つ任意のストリームからデータが含まれるかどうか、 **CopyProtect**フラグを設定、ドライバーは、再生キャプチャのパスをミュートする必要があります。

DRM 準拠オーディオ ドライバーをサポートする必要があります、 [IDrmAudioStream](https://msdn.microsoft.com/library/windows/hardware/ff536568)オブジェクトのインターフェイスの WaveCyclic と WavePci ミニポート ドライバー、オーディオ データを表示するためのシンクのピンを公開することができます。 参照を取得するために、 **IDrmAudioStream**ドライバー、DRMK 呼び出しからのオブジェクト、 **QueryInterface**ピン メソッド。 Pin が型のインターフェイス[IMiniportWaveCyclicStream](https://msdn.microsoft.com/library/windows/hardware/ff536715)または[IMiniportWavePciStream](https://msdn.microsoft.com/library/windows/hardware/ff536725)します。 **IDrmAudioStream**インターフェイスは、1 つのメソッドをサポートしている[ **IDrmAudioStream::SetContentId** ](https://msdn.microsoft.com/library/windows/hardware/ff536570) (3 つだけでなく**IUnknown**メソッド)。 DRMK を呼び出すと**SetContentId**、コンテンツの ID と、ドライバーは、暗証番号 (pin) のデータ ストリームを関連付けます、コンテンツの権限を渡します。

WaveCyclic または WavePci ミニポート ドライバー Drmk.sys で DRM 関数を直接呼び出す代わりにを介して DRM 関数にアクセスできます、 [IDrmPort2](https://msdn.microsoft.com/library/windows/hardware/ff536573)インターフェイス (**IDrmPort2**は基本クラスから派生[IDrmPort](https://msdn.microsoft.com/library/windows/hardware/ff536571))。 WaveCyclic と WavePci ポート ドライバーがサポートする Microsoft Windows XP 以降では、 **IDrmPort2**します。 ミニポート ドライバー、ポート ドライバーへの参照を取得する**IDrmPort2**呼び出してポート オブジェクトのインターフェイス**QueryInterface** REFIID iid メソッド\_IDrmPort2 します。

オーディオ ドライバーでは、ハードウェアの混合はサポートし、同時に複数の入力データ ストリームを処理することができます。 この種類のドライバーする必要がありますの追跡個別のストリームと複合コンテンツの権限をすべてのストリームの両方のコンテンツ Id。 ドライバー呼び出し[ **IDrmPort::CreateContentMixed** ](https://msdn.microsoft.com/library/windows/hardware/ff536581)混合ストリームの複合の権利をそのストリームを識別するためにコンテンツ ID を作成します。 呼び出す必要がありますが、ドライバーでは、コンテンツ ID の使用が完了したら、 [ **IDrmPort::DestroyContent** ](https://msdn.microsoft.com/library/windows/hardware/ff536583)コンテンツ ID を削除するには

入力ストリームを追加または、ミキサー アプリケーションから削除するたびに、ドライバーする必要があります古いミックスのコンテンツ ID を削除して新しい組み合わせの場合は、新しいコンテンツ ID を作成します。 古いコンテンツ ID を削除する前に、ドライバーする必要があります最初を正常に転送が以前の転送先に古いコンテンツの id。 すべてのストリームに新しいコンテンツ ID 詳細については、次を参照してください。 [DRM コンテンツ Id の転送](forwarding-drm-content-ids.md)します。

 

 




