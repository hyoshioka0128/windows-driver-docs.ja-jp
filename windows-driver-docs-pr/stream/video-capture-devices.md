---
title: ビデオ キャプチャ デバイス
description: ビデオ キャプチャ デバイス
ms.assetid: ed02e6c8-fd82-488b-a0dc-8e83a842bcc4
keywords:
- ビデオの WDK AVStream のキャプチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3615fe8bbe8c95475f9fa52c35694d7e57cb70ed
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557408"
---
# <a name="video-capture-devices"></a>ビデオ キャプチャ デバイス


このセクションでは、ビデオ キャプチャ ミニドライバーは、次の Windows Driver Model (WDM) アーキテクチャを作成する方法について説明します。 説明する概念に関する知識と想定して[カーネル ストリーミング](kernel-streaming.md)します。 オーディオのみのデバイス用のミニドライバーを作成する方法について、[オーディオ デバイスの設計ガイド](https://msdn.microsoft.com/library/windows/hardware/ff536191)します。

DVD、MPEG デコーダー、ビデオ デコーダーとチューナー、ビデオ ポート拡張機能 (VPEs)、および 1 つのアダプターでのオーディオ コーデックの統合により、これらすべてのデバイスをサポートし、リソースの競合を処理する統一されたドライバー モデルには、開発作業が簡略化します。

[AVStream](avstream-minidrivers-design-guide.md)と[Stream クラス](https://msdn.microsoft.com/library/windows/hardware/ff568275)両方のインターフェイスが統合されたデバイスのサポートを提供するフレームワークを提供します。 これらのインターフェイスは、カーネル モード ドライバーの間のデータ転送をサポートします。 これらのデータ転送は、スレッド ユーザー モードに移行する必要ありません、パフォーマンスに影響を回避します。

両方のインターフェイスは、統一されたモデルの標準とカスタム データ型のストリーミングをサポートします。 Microsoft では、標準的なデバイスのプロパティ セットを定義します。 ベンダーは、必要な場合、追加のプロパティのセットを提供できます。

すべての新しいビデオ キャプチャ ドライバーが AVStream インターフェイスを使用することをお勧めします。 Microsoft は、旧バージョンとの互換性のための Stream クラス インターフェイスを提供します。 ただし、Stream クラスのインターフェイスは廃止されていますと Microsoft は、さらに開発を廃止します。

**注**  :このセクションでは古い形式の Windows のビデオ (VfW) テクノロジを説明しません。 VfW は、ディスクにビデオをキャプチャするために最適化されていました。 ビデオ会議に重要な機能では、テレビの視聴、ビデオのフィールド、および補助データ ストリームのキャプチャは不足している VfW アーキテクチャです。 これらの制限を回避するためにベンダーは VfW に専用の拡張機能が追加されます。 ただし、標準化されたインターフェイスは、なし、これらの機能を使用するアプリケーションはハードウェアに依存するコードを含める必要があります。
VfW と WDM ドライバー モデルをブリッジするには、Microsoft には、オペレーティング システムの一部として VfW-WDM をマッパーが用意されています。 このコンポーネントには、レガシ アプリケーションの VfW VfW ドライバーとして表示する WDM ドライバーができるようにします。

 

このセクションの内容:

[ビデオのキャプチャの概要](video-capture-overview.md)

[ビデオ キャプチャ サポートを実装します。](implementing-video-capture-support.md)

 

 




