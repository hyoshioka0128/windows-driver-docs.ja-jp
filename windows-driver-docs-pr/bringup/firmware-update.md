---
title: ファームウェアの更新
description: Microsoft Windows Update (WU) および UEFI UpdateCapsule 関数を使用してシステムとデバイスのファームウェア更新を配信するためのサポートについて説明します。
ms.date: 05/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2d65fe0c7ee496e9d75d2d3d90fac93c9bbc8b50
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574883"
---
# <a name="firmware-update"></a>ファームウェアの更新

Windows のシステムとデバイス ファームウェアの更新プログラムを提供する Microsoft Windows Update (WU) を使用して配布するドライバー パッケージにラップされたに渡され、UEFI で処理のプラットフォームをサポートしている**UpdateCapsule**関数. このプラットフォームにより、一貫性、信頼性の高いファームウェアの更新プログラムのエクスペリエンスと重要なシステムのエンドユーザー向けのファームウェアの更新プログラムを配信する機能が向上します。

この機能は、早い段階では、Windows 8.1 の利用にされています。 ただし、いくつかの最近の変更が必要ファームウェア プロバイダーは、モデルと共にコンピューター ハードウェア ID (CHID) を対象とする結合一意 EFI システム リソース テーブル (ESRT) UEFI\_RES\\一意 {ID} 特定のシステムをより正確にターゲットにまたは、システムの範囲。

一意の ID 一意 {ID}、ESRT では、重要です。 UNIQUE ID + CHID の目的は、ファームウェアのプロバイダーが Windows の更新 (WU) 経由で、一意の ID + CHID に一致するすべてのシステムに展開される更新プログラム パッケージ/BIOS ファームウェアを作成できるようにです。 Microsoft では、ファームウェア パッケージを検証するためのメカニズムがあり、ペイロードが改ざんされていないことを確認するファームウェア プロバイダー (パッケージの作成者) に依存です。 これは、暗号によって検証する必要があります。チェックサムやその他の Crc が検証ではありません。 ペイロードには、検証が失敗した場合は、失敗し、」の説明に従って、ESRT で状態を記録にする必要があります[ESRT テーブル定義](https://docs.microsoft.com/windows-hardware/drivers/bringup/esrt-table-definition)します。

> [!NOTE]
> OEM、ODM、および ESRT {一意 ID} を作成することに携わる人、ESRT が {一意の id} は、あらかじめ設定されていることを検出するが場合と見なさないでください一意であります。 {一意 id} ESRT を設定し、この後で使用するために記録します。 Microsoft では、このようなシナリオの一意の ID を作成する方法のガイダンスがあります。 このガイダンスは、ダウンロード可能なドキュメントには[ドライバー発行ワークフローを Windows 10](http://download.microsoft.com/download/B/A/8/BA89DCE0-DB25-4425-9EFF-1037E0BA06F9/windows10_driver_publishing_workflow.docx)します。



## <a name="in-this-section"></a>このセクションの内容

[構築し、ファームウェア パッケージを Windows Update (WU) の提出](build-and-submit-a-firmware-package-to-windows-update.md)

[CHID を使用してシステムを対象します。](target-a-system-using-chid.md)

[ファームウェアのユーザー エクスペリエンス (UX) のベスト プラクティス](firmware-user-experience-best-practices.md)

[ファームウェア更新の検証テスト](firmware-update-validation-testing.md)






