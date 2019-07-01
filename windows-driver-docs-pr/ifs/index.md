---
title: ファイル システム フィルターの概要
description: Windows のファイル システムは、ストレージ システムの上で動作するファイル システム ドライバーとして実装されます。
ms.assetid: 62DE75F7-0211-4173-AF45-84B2DDFDC95C
ms.date: 05/31/2019
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 44d5022276a3fdc5002ccd52d2ea5e5da86dfce6
ms.sourcegitcommit: 95e3fd15d9c00a341e774d58a927856d750a35e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2019
ms.locfileid: "67410014"
---
# <a name="file-systems-driver-design-guide"></a>ファイル システム ドライバー設計ガイド

WDK のこのセクションでは、ファイル システムおよびフィルター ドライバー (ミニフィルター) に関連する概念の情報を提供します。 ドライバーで実装または呼び出しできるプログラミング インターフェイスについては、 [ファイル システムのプログラミング リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_ifsk/)に関するページを参照してください。

Windows のファイル システムは、ストレージ システムの上で動作するファイル システム ドライバーとして実装されます。 Windows の各ファイル システムは、信頼性の高いデータ ストレージを与えるように設計されています。さまざまな機能でユーザーの要件を満たします。 Windows の各標準ファイル システムの機能比較は、「[File System Functionality Comparison](https://docs.microsoft.com/windows/desktop/FileIO/filesystem-functionality-comparison)」 (ファイル システムの機能比較) にあります。 Windows Server 2012 の新機能は ReFS です。 ReFS は、スケーラブルに大容量をサポートし、ディスク上のデータ破損を検出して、修復できるファイル システムです。

Windows 提供のものに加え、新しいファイル システム ドライバーを作成する必要はおそらくありません。 ファイル システムとファイル システム フィルター ドライバーによって、既存のファイル システムの操作を変更するために必要なあらゆる動作をカスタマイズできます。

## <a name="span-idfilesystemfilterdriverdevelopmentspanspan-idfilesystemfilterdriverdevelopmentspanspan-idfilesystemfilterdriverdevelopmentspanfile-system-filter-driver-development"></a><span id="File_System_Filter_Driver_Development"></span><span id="file_system_filter_driver_development"></span><span id="FILE_SYSTEM_FILTER_DRIVER_DEVELOPMENT"></span>ファイル システム フィルター ドライバー開発

ファイル システム フィルター ドライバーは、ファイル システムまたは別のファイル システム フィルター ドライバーを対象にした要求をインターセプトします。 要求が当初の宛先に届く前にインターセプトすることで、フィルター ドライバーは、要求の当初の宛先によって提供する機能を拡張するか、その代わりをすることができます。 ファイル システムとファイル システム フィルター ドライバーの例には、アンチウイルス フィルター、バックアップ エージェント、暗号化製品などがあります。

ファイル システム フィルタリング サービスは、Windows の[フィルター マネージャー](filter-manager-and-minifilter-driver-architecture.md)から利用できます。 フィルター マネージャーからは、ファイル システムとファイル システム フィルター ドライバーを開発するためのフレームワークが提供されます。複雑なファイル I/O をすべて管理する必要がありません。 フィルター マネージャーはサードパーティ フィルター ドライバーの開発を簡単にします。また、階層を割り当てることで負荷の順序を管理するなど、旧式フィルター ドライバー モデルに存在するさまざまな問題を解決します。 フィルター マネージャー モデルに対して開発されたフィルター ドライバーはミニフィルターと呼ばれています。 すべてのミニフィルター ドライバーには階層が割り当てられています。階層は、I/O スタックの他のミニフィルターに相対的にミニフィルターが読み込まれる場所を決定する一意の識別子です。 階層は Microsoft によって割り当てられ、管理されます。

## <a name="span-idfilesystemfilterdrivercertificationspanspan-idfilesystemfilterdrivercertificationspanspan-idfilesystemfilterdrivercertificationspanfile-system-filter-driver-certification"></a><span id="File_System_Filter_Driver_Certification"></span><span id="file_system_filter_driver_certification"></span><span id="FILE_SYSTEM_FILTER_DRIVER_CERTIFICATION"></span>ファイル システム フィルター ドライバー認定

ファイル システムとファイル システム フィルター ドライバーの認定情報は [Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613) にあります。 ファイル システムとファイル システム フィルター ドライバーのテストは HCK の [Filter.Driver](https://docs.microsoft.com/previous-versions/windows/hardware/hck/jj124779(v=vs.85)) カテゴリにあります。

## <a name="span-idfilesystemfilterdriverdeveloperresourcesspanspan-idfilesystemfilterdriverdeveloperresourcesspanspan-idfilesystemfilterdriverdeveloperresourcesspanfile-system-filter-driver-developer-resources"></a><span id="File_System_Filter_Driver_Developer_Resources"></span><span id="file_system_filter_driver_developer_resources"></span><span id="FILE_SYSTEM_FILTER_DRIVER_DEVELOPER_RESOURCES"></span>ファイル システム フィルター ドライバー開発者リソース

Microsoft に高度の割り当てを依頼するには、ミニフィルターの高度割り当てを求める電子メールを送信してください。 [ミニフィルター高度要求](minifilter-altitude-request.md)の指示に従い、要求を送信します。

再解析ポイントを使用するフィルター ドライバーの ID を取得するには、「[Reparse Point Request](reparse-point-tag-request.md)」 (再解析ポイントの依頼) の手順に従います。

ファイル システムとフィルター ドライバーの開発については、NTFSD ニュースグループを購読できます。 このグループは [NT ファイル システム ドライバー ニュースグループ](https://go.microsoft.com/fwlink/p/?LinkId=620898)にあります。

OSR の "Developing File Systems for Windows" セミナーは、ファイル システムの開発と、ファイル システムとファイル システム フィルター ドライバーを取り上げています。 「[Training for IFS Developers](https://go.microsoft.com/fwlink/p/?linkid=50692)」 (IFS 開発者のためのトレーニング) を参照してください。
