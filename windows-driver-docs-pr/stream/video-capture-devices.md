---
title: ビデオ キャプチャ デバイス
description: ビデオ キャプチャ デバイス
ms.assetid: ed02e6c8-fd82-488b-a0dc-8e83a842bcc4
keywords:
- ビデオをキャプチャする WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e7c09b0afc965b3f6e62b73ee095f157f304b9f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844933"
---
# <a name="video-capture-devices"></a>ビデオ キャプチャ デバイス


このセクションでは、Windows Driver Model (WDM) アーキテクチャに従った video capture ミニドライバーを作成する方法について説明します。 [カーネルストリーミング](kernel-streaming.md)で説明されている概念を理解していることを前提としています。 オーディオ専用デバイス用のミニドライバーの作成の詳細については、「[オーディオデバイス設計ガイド」](https://docs.microsoft.com/windows-hardware/drivers/audio/index)を参照してください。

DVD、MPEG デコーダー、ビデオデコーダーとチューナー、ビデオポート拡張 (VPEs)、オーディオコーデックを1つのアダプターに統合することで、これらすべてのデバイスをサポートし、リソースの競合を処理する統合されたドライバーモデルにより、開発作業が簡単になります。

[Avstream](avstream-minidrivers-design-guide.md)と[Stream クラス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)のインターフェイスはどちらも、統合デバイスのサポートを提供するフレームワークを提供します。 これらのインターフェイスは、カーネルモードドライバー間のデータ転送をサポートしています。 これらのデータ転送では、スレッドをユーザーモードに移行する必要がないため、パフォーマンスの低下を回避できます。

どちらのインターフェイスも、標準およびカスタムのデータ型に対して、統一されたストリーミングモデルをサポートします。 Microsoft では、ほとんどの標準デバイスのプロパティセットを定義しています。 ベンダーは、必要に応じて追加のプロパティセットを提供できます。

すべての新しいビデオキャプチャドライバーで AVStream インターフェイスを使用することをお勧めします。 Microsoft では、旧バージョンとの互換性のためにストリームクラスインターフェイスを提供しています。 ただし、Stream クラスインターフェイスは互換性のために残されていますが、マイクロソフトはさらなる開発を廃止しました。

**注**  : このセクションでは、Windows 用の古いビデオ (VfW) テクノロジについては説明しません。 VfW は、ムービーをディスクにキャプチャするために最適化されました。 ビデオ会議、テレビ番組、ビデオフィールドのキャプチャ、および補助データストリームに重要な機能は、VfW アーキテクチャにはありません。 これらの制限を回避するために、ベンダーは VfW に独自の拡張機能を追加しました。 ただし、標準化されたインターフェイスを使用しない場合、これらの機能を使用するアプリケーションにはハードウェアに依存するコードを含める必要があります。
VfW および WDM ドライバーモデルをブリッジするために、Microsoft はオペレーティングシステムの一部として VfW と WDM のマッパーを提供しています。 このコンポーネントにより、WDM ドライバーがレガシ VfW アプリケーションの VfW ドライバーとして表示されるようになります。

 

このセクションの内容:

[ビデオキャプチャの概要](video-capture-overview.md)

[ビデオキャプチャサポートの実装](implementing-video-capture-support.md)

 

 




