---
title: ドライバー ファイル内の埋め込み署名
description: ドライバー ファイル内の埋め込み署名
ms.assetid: 21941c7b-4f9a-424c-9984-3048a53398b6
keywords:
- 埋め込み署名 WDK ドライバーの署名
- ドライバー WDK、埋め込みの署名
- 埋め込みドライバー WDK を署名するには、
- デジタル署名 WDK、埋め込まれました。
- 埋め込まれた、WDK の署名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 021949f7a3d1efac132fbcbcb92e4158ec05690e
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393437"
---
# <a name="embedded-signatures-in-a-driver-file"></a>ドライバー ファイル内の埋め込み署名


64 ビット バージョンの Windows Vista および以降のバージョンの Windows では、カーネル モード コード署名の要件が埋め込まれたあります[ソフトウェア発行元証明書 (SPC)](software-publisher-certificate.md)署名します。 埋め込みの署名は、ドライバーはブート開始ドライバーの必要はありません。

**注**  デスクトップ エディション (Home、Pro、Enterprise、および Education) および Windows Server 2016 カーネル モード ドライバー用の Windows 10 は Windows ハードウェア デベロッパー センター ダッシュ ボード Windows ハードウェア デベロッパー センター ダッシュ ボードを署名する必要がありますEV 証明書が必要です。 これらの変更に関する詳細については、次を参照してください。 [Windows 10 でドライバー署名の変更](https://techcommunity.microsoft.com/t5/Windows-Hardware-Certification/bg-p/WindowsHardwareCertification)します。

 

検索するシステムのローダーの必要性がないために、システムの起動時に膨大な時間を保存します埋め込みの署名を持つ、[カタログ ファイル](catalog-files.md)システムの起動時にドライバー。 Windows Vista または Windows の以降のバージョンを実行している、一般的なコンピューターでは、カタログのルート ストアに多数の別のカタログ ファイルがあります ( *% システム\\CatRoot*)。 ドライバー ファイルの拇印を検証する適切なカタログ ファイルを検索すると、かなりの時間が必要です。

カーネル モード コード署名ポリシーによって適用される、読み込み時の署名要件だけでなく、プラグ アンド プレイ (PnP) デバイスのインストールは、インストール時の署名の要件を強制します。 準拠する、 [PnP デバイスのインストール要件を署名](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)Windows Vista および Windows での以降のバージョンの[ドライバー パッケージ](driver-packages.md)は PnP デバイスは、署名済みカタログ ファイルがある必要です。

埋め込み署名に影響を及ぼさないカタログ ファイルの署名カタログ ファイルと埋め込み署名の拇印に選択的に格納されている拇印が、ドライバー ファイルの署名部分を除外するためです。

ドライバー ファイルに署名を使用して、 [SignTool](installing-a-catalog-file-by-using-signtool.md)ツール。

 

 





