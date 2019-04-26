---
title: ファームウェア ユーザー エクスペリエンス (UX) のベスト プラクティス
description: ファームウェア ユーザー エクスペリエンス (UX) のベスト プラクティス
ms.date: 05/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: 402ef054d1a9df0e1f5e113384f6a5350886c245
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337616"
---
# <a name="firmware-user-experience-ux-best-practices"></a>ファームウェア ユーザー エクスペリエンス (UX) のベスト プラクティス


システム ファームウェアの更新では、そのマシンの使用を継続するがあります。 Microsoft は、ファームウェアの更新プログラムが安全に配信され、インストールが中断されたことを確認したいです。 これを行うより詳細に説明が記載されている次のガイドラインを推奨、**の関連リソース**セクション。

1.  進行状況バー/インジケーター: システムが更新プログラムをインストールすることです。

2.  Windows ブート ローダー **UpdateCapsule**関数はユーザーのメッセージを含むビットマップを提供します。

3.  UEFI AC 電源、または十分なバッテリの寿命 (RSOC) 確認するかを ESRT に記録されたエラー コードで失敗します。

**の関連リソース**最新ファームウェア UX のガイダンスについてはリンク。

## <a name="related-resources"></a>関連リソース

[Windows の UEFI ファームウェアを更新するプラットフォーム](https://docs.microsoft.com/windows-hardware/drivers/bringup/windows-uefi-firmware-update-platform)

[シームレスな危機防止と回復](https://docs.microsoft.com/windows-hardware/drivers/bringup/seamless-crisis-prevention-and-recovery)

[ユーザーは、UEFI ファームウェアの更新プログラムをエクスペリエンスします。](https://docs.microsoft.com/windows-hardware/drivers/bringup/user-experience-for-uefi-firmware-updates)

[起動画面のコンポーネント](https://docs.microsoft.com/windows-hardware/drivers/bringup/boot-screen-components)

[ESRT テーブルの定義](https://docs.microsoft.com/windows-hardware/drivers/bringup/esrt-table-definition)

[Windows の UEFI ファームウェア更新プラットフォーム機能を検証しています](https://docs.microsoft.com/windows-hardware/manufacture/desktop/validating-windows-uefi-firmware-update-platform-functionality)




