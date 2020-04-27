---
title: ファイル システム ドライバー設計ガイド
description: ファイル システム ドライバー設計ガイド
ms.assetid: 62DE75F7-0211-4173-AF45-84B2DDFDC95C
ms.date: 01/10/2020
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 97b237f5794d4ee38e390def974c18cc6a3e7719
ms.sourcegitcommit: 988d100e4d3b218a59fdac034d39a1816d145c85
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2020
ms.locfileid: "78910383"
---
# <a name="file-systems-driver-design-guide"></a>ファイル システム ドライバー設計ガイド

WDK のこのセクションでは、ファイル システムおよびフィルター ドライバー (ミニフィルター) に関連する概念の情報を提供します。 ドライバーで実装または呼び出しできるインターフェイスを説明する参照ページについては、[ファイル システムのプログラミング リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_ifsk/)に関するページを参照してください。

## <a name="file-systems"></a>ファイル システム

Windows のファイル システムは、ストレージ システムの上で動作するファイル システム ドライバーとして実装されます。

Windows の各システム提供のファイル システムは、信頼性の高いデータ ストレージを与えるように設計されています。さまざまな機能でユーザーの要件を満たします。 Windows で使用できる標準のファイル システムには、NTFS、ExFAT、UDF、FAT32 があります。 これらの各ファイル システムの機能比較については、「[ファイル システムの機能比較](https://docs.microsoft.com/windows/desktop/FileIO/filesystem-functionality-comparison)」をご覧ください。 また、Windows Server 2012 以降のバージョンで使用できる [Resilient File System](https://docs.microsoft.com/windows-server/storage/refs/refs-overview) (ReFS) は、スケーラブルに大容量をサポートし、ディスク上のデータ破損を検出して、修復できます。

新しいファイル システム ドライバーを開発する必要はおそらくありません。新しいファイル システム ドライバーの要件と仕様は予測できません。 そのため、この設計ガイドではファイル システムの開発については説明しません。 Windows で使用できるファイル システ ムドライバー以外の新しいファイル システム ドライバーを開発する必要がある場合は、サンプル コードをモデルとして使用できます (詳細については以下を参照してください)。

## <a name="file-system-filter-drivers"></a>ファイル システム フィルター ドライバー

ファイル システム フィルター ドライバーは、ファイル システムまたは別のファイル システム フィルター ドライバーを対象にした要求をインターセプトします。 要求が当初の宛先に届く前にインターセプトすることで、フィルター ドライバーは、要求の当初の宛先によって提供する機能を拡張するか、その代わりをすることができます。 フィルター ドライバーの例を次に示します。

- ウイルス対策フィルター
- バックアップ エージェント
- 暗号化製品

ファイル システム フィルタリング サービスは、Windows のシステム提供の[フィルター マネージャー](https://docs.microsoft.com/windows-hardware/drivers/ifs/filter-manager-concepts)から利用できます。 フィルター マネージャーからは、フィルター ドライバーを開発するためのフレームワークが提供されます。複雑なファイル I/O をすべて管理する必要がありません。 フィルター マネージャーはサードパーティ フィルター ドライバーの開発を簡単にします。また、階層を割り当てることで負荷の順序を管理するなど、レガシ フィルター ドライバー モデルに関するさまざまな問題を解決します。

フィルター マネージャー モデルに対して開発されたフィルター ドライバーはミニフィルターと呼ばれています。 すべてのミニフィルター ドライバーには階層が割り当てられています。階層は、I/O スタックの他のミニフィルターに相対的にミニフィルターが読み込まれる場所を決定する一意の識別子です。 階層は Microsoft によって割り当てられ、管理されます。

## <a name="file-system-and-filter-sample-code"></a>ファイル システムとフィルター サンプル コード

ファイル システムの開発やファイル システム フィルター ドライバーの開発のサンプルなど、いくつかの Windows ドライバーのサンプルが用意されています。 完全な一覧については、「[Windows ドライバー サンプル](https://docs.microsoft.com/windows-hardware/drivers/samples)」を参照してください。

## <a name="file-system-filter-driver-certification"></a>ファイル システム フィルター ドライバー認定

ファイル システムとファイル システム フィルター ドライバーの認定情報は [Windows ハードウェア ラボ キット (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613) にあります。 ファイル システムとファイル システム フィルター ドライバーのテストは HCK の [Filter.Driver](https://docs.microsoft.com/previous-versions/windows/hardware/hck/jj124779(v=vs.85)) カテゴリにあります。

## <a name="additional-resources"></a>その他の資料

このドキュメントと上記のサンプル コードと共に、次の追加リソースを利用できます。

- Microsoft に高度の割り当てを依頼するには、ミニフィルターの高度割り当てを求める電子メールを送信してください。 [ミニフィルター高度要求](minifilter-altitude-request.md)の指示に従い、要求を送信します。

- 再解析ポイントを使用するフィルター ドライバーの ID を取得するには、「[Reparse Point Request](reparse-point-tag-request.md)」 (再解析ポイントの依頼) の手順に従います。

- [OSR](https://go.microsoft.com/fwlink/p/?linkid=50692) は、ファイル システム ミニフィルター開発用のさまざまなリソースを提供します。これには、NTFDS フォーラムなど、セミナーやコミュニティのディスカッション フォーラムなどが含まれます。
