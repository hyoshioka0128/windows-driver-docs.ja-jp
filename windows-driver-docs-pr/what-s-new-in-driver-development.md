---
title: What's new in driver development
description: このセクションでは、Windows 10 でのドライバー開発に関する新機能について説明します。
ms.assetid: 5502AAF9-2400-4338-A646-C746B29F9A44
ms.date: 04/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: 678be02ff0d40401e88776b1eef8aa09a921c0ee
ms.sourcegitcommit: d395d4b36f39d3557adda53735a4fdc8745a6408
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83642594"
---
# <a name="whats-new-in-driver-development"></a><a name="top"></a>ドライバー開発に関する最新情報

このセクションでは、Windows 10 での Windows ドライバー開発に関する新機能と更新された機能について説明します。

## <a name="whats-new-in-windows-10-version-2004-latest"></a>Windows 10 バージョン 2004 (最新版) の最新情報

このセクションでは、Windows 10 バージョン 2004 (Windows 10 May 2020 Update) でのドライバー開発に関する新機能と更新された機能について説明します。

### <a name="windows-drivers"></a>Windows ドライバー

Windows 10 バージョン 2004 は、ユニバーサル ドライバーの移行リリースです。 このリリースでは、依然としてユニバーサル ドライバーがありますが、Windows ドライバーに置き換えられつつあります。 Windows ドライバーは、追加の要件を備えたユニバーサル ドライバーです。

Windows ドライバーは、Windows デスクトップ ドライバーとは区別されます。 Windows ドライバーは Windows 10X および Windows 10 デスクトップ エディションで実行されますが、Windows デスクトップ ドライバーは Windows 10 デスクトップ エディションでのみ実行されます。

バージョン 2004 リリースではユニバーサル ドライバーへの変更は必要ありませんが、今後の変更に向けて計画を立てられるように、ドキュメントが公開されています。

Windows ドライバーをビルド、インストール、展開、デバッグする方法については、「[Windows ドライバーの概要](https://docs.microsoft.com/windows-hardware/drivers/develop/getting-started-with-windows-drivers)」を参照してください。

### <a name="windows-hardware-error-architecture-whea"></a>Windows Hardware Error Architecture (WHEA)

WHEA には、新しいインターフェイス (v2) が含まれています。 エラー ソースを登録し、エラーをレポートする方法については、「[Windows 10 で WHEA を使用する](whea/using-whea-on-windows-10.md)」を参照してください。

### <a name="display-and-graphics-drivers"></a>ディスプレイとグラフィック ドライバー

Windows 10 バージョン 2004 では、D3D12 メッシュ シェーダー サポート、サンプラー サポート、レイトレーシング拡張機能、ビデオ モーション予測、およびビデオ保護されたリソース サポートを含む、いくつかの新しい強化されたディスプレイおよびグラフィックス ドライバー機能が利用可能です。 これらの新機能の詳細については、「[Windows 10 ディスプレイおよびグラフィックス ドライバーの新機能](https://docs.microsoft.com/windows-hardware/drivers/display/what-s-new-for-windows-10-display-and-graphics-drivers)」を参照してください。

### <a name="storage-drivers"></a>ストレージ ドライバー

ストレージ ミニポート ドライバーでは、デバイスをリセットする機能など、デバイスの内部状態に関する詳細情報を取得および設定できるようになりました。 まずは、[**IOCTL_STORAGE_GET_DEVICE_INTERNAL_LOG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_get_device_internal_log) および [**StorPortHardwareReset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storporthardwarereset) をご覧ください。

## <a name="related-topics"></a>関連トピック

過去の Windows リリースのドライバー関連最新情報については、以下のページを参照してください。

* [Windows 10 バージョン 1903 のドライバー開発の変更点](driver-changes-for-windows-10-version-1903.md)
* [Windows 10 バージョン 1809 のドライバー開発の変更点](driver-changes-for-windows-10-version-1809.md)
* [Windows 10 バージョン 1803 のドライバー開発の変更点](driver-changes-for-windows-10-version-1803.md)
* [Windows 10 バージョン 1709 のドライバー開発の変更点](driver-changes-for-windows-10-version-1709.md)

[ページのトップへ](#top)

## <a name="deprecated-features"></a>推奨されなくなった機能

次の表では、Windows 10 で削除された Windows ドライバー開発の機能について説明します。

| ドライバーのテクノロジ | 機能 | 非推奨になったバージョン |
|---|---|---|
| GNSS/位置情報 | [Windows 8.1 用の位置情報ドライバー サンプル](https://docs.microsoft.com/windows-hardware/drivers/gnss/sensors-geolocation-driver-sample)とその関連ドキュメント | Windows 10 バージョン 1709 |
| 通信事業者のシナリオ (ネットワーク) | [AllowStandardUserPinUnlock](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/allowstandarduserpinunlock) | Windows 10 バージョン 1709 |
| スキャン/イメージ | [WSD (Web Services for Devices) Challenger](https://docs.microsoft.com/windows-hardware/drivers/image/challenging-a-disconnected-scanner-with-the-wsd-challenger) 機能とその関連ドキュメント | Windows 10 バージョン 1709 |
|通信事業者| Sysdev メタデータ パッケージを使ったモバイル ブロードバンド アプリ エクスペリエンスのアプリは非推奨になりました。代わりに MO UWP APPS と COSA が推奨されます。 | Windows 10 バージョン 1803|
