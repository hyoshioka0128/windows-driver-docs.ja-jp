---
title: Windows での ACPI サポートの概要
description: このトピックでは、SoC ベースのプラットフォームで Windows をサポートするために必要な ACPI 5.0 の機能の一部をまとめています。
ms.assetid: BECFB30B-541B-420E-85F3-773292066A90
ms.date: 05/22/2020
ms.localizationpriority: medium
ms.openlocfilehash: a394640485adbce7211c44dc89192fb763c93715
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851718"
---
# <a name="summary-of-acpi-support-in-windows"></a>Windows での ACPI サポートの概要

このトピックでは、SoC ベースのプラットフォームで Windows をサポートするために必要な、Advanced Configuration and Power Interface (ACPI) 5.0 の機能の一部をまとめています。

| 機能 | ACPI 5.0 仕様のセクション | Notes |
| --- | --- | --- |
| システムの説明テーブル | 5.2.5 | ルートシステムの説明ポインター (RSDP) |
| | 5.2.7、5.2.8 | ルート (RSDT) または拡張 (XSDT) システムの説明テーブルのいずれか |
| | 5.2.9 | ACPI の説明の表 (FADT) を修正します。 |
| | 5.2.12 | 複数の APIC Description テーブル (MADT) |
| | 5.2.24 | 汎用タイマーの説明の表 (GTDT) |
| | 5.2.6  | コアシステムリソーステーブル (CSRT) の[仕様](https://acpica.org/related-documents) |
| | 5.2.6  | デバッグポートテーブル 2 (DBG2) の[仕様](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn639131(v=vs.85)) |
| | 5.2.11.1 | 区別されるシステムの説明テーブル (DSDT) |
| | 5.2.11.2 | セカンダリシステムの説明の表 (SSDT) |
| デバイス管理 | 6.1 | デバイス識別オブジェクト |
| | 6.2 | デバイス構成オブジェクト |
| GPIO | 5.6.5.1 | GPIO コントローラーデバイス |
| | 5.6.5 | GPIO シグナル状態の ACPI イベント |
| | 6.4.3.8.1, 19.5.53, 19.5.54 | GPIO リソース記述子とマクロ |
| | 5.5.2.4.4 | GeneralPurposeIO OpRegions |
| SPB (Simple Peripheral Bus) | 6.4.3.8.2, 19.5.55, 19.5.118, 19.5.134 | SPB リソース記述子とマクロ |
| | | GenericSerialBus OpRegions |
| デバイス電源管理 | 3.3 | |
| | 7.1 | 電源リソース |
| | 7.2 | デバイスの電源管理オブジェクト |
| ACPI で定義されたデバイス | 9.0、10 | |
| | 9.5 | コントロールメソッドの電源ボタン |
| | 9.4 | コントロールメソッド Lid デバイス |
| | 10.2 | 制御方式のバッテリデバイス |
| | 9.18 | 制御メソッドの時刻とアラームデバイス |
| | 11 | 温度ゾーン |
| デバイス固有のサポート | 8.4 | [プロセッサ] |
| | 付録 B | 表示 |
| | 6.1.8、9.13 | USB |
| | | SD バス |
| | | カメラ |
| | | HID-I-I ² C デバイス |
| | 3.2.1、4.8.2.2.1.2、4.8.2.2.1.3 | ボタン |
| | | PC センサーのドッキングとコンバーチブル |
