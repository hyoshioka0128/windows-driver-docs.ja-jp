---
title: ドライバー ファイル内の埋め込み署名
description: ドライバー ファイル内の埋め込み署名
ms.assetid: 21941c7b-4f9a-424c-9984-3048a53398b6
keywords:
- 組み込み署名 WDK ドライバー署名
- ドライバー署名 WDK、埋め込み
- 署名ドライバー (WDK)、埋め込み
- デジタル署名 WDK、埋め込み
- 署名 WDK、埋め込み
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: abefc35277c7657c6271c49aa258ee634e5e86fc
ms.sourcegitcommit: e1f02bc9a982eefa1e326c95d3aca5ecc68581ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73721622"
---
# <a name="embedded-signatures-in-a-driver-file"></a>ドライバー ファイル内の埋め込み署名


Windows Vista 以降のバージョンの windows 64 では、カーネルモードのコード署名の要件に埋め込みの[ソフトウェア発行元証明書 (SPC)](software-publisher-certificate.md)署名が必要です。 ブート開始ドライバー以外のドライバーでは、埋め込み署名は必要ありません。

> [!NOTE]
> Windows 10 for desktop エディション (Home、Pro、Enterprise、および教育) と Windows Server 2016 カーネルモードドライバーは、EV 証明書を必要とする Windows Hardware Dev Center ダッシュボードによって署名されている必要があります。 これらの変更の詳細については、「 [Windows 10 でのドライバー署名の変更点](https://techcommunity.microsoft.com/t5/Windows-Hardware-Certification/Driver-Signing-changes-in-Windows-10-version-1607/ba-p/364894)」を参照してください。

 

システムの起動時にドライバーの[カタログファイル](catalog-files.md)を検索する必要がないため、署名が埋め込まれていると、システムの起動時にかなりの時間が節約されます。 一般的なコンピューターでは、カタログルートストア ( *% System%\\CatRoot*) に多数の異なるカタログファイルが存在する場合があります。 正しいカタログファイルを検索して、ドライバーファイルの拇印を確認するには、かなりの時間が必要になることがあります。

カーネルモードのコード署名ポリシーによって適用される読み込み時の署名要件に加えて、プラグアンドプレイ (PnP) デバイスのインストールでも、インストール時の署名要件が適用されます。 Windows Vista 以降のバージョンの Windows では、 [pnp デバイスのインストール署名の要件](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)に準拠するために、pnp デバイスの[ドライバーパッケージ](driver-packages.md)に署名済みのカタログファイルが必要です。

埋め込み署名は、カタログファイルの署名には影響しません。これは、カタログファイルに含まれる拇印と埋め込み署名の拇印が選択的にドライバーファイルの署名部分を除外するためです。

ドライバーファイルは、 [SignTool](installing-a-catalog-file-by-using-signtool.md)ツールを使用して署名されます。

 

 





