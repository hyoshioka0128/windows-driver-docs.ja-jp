---
title: ファームウェアの測定値
description: ファームウェアの測定値では、ファームウェア ドライバーのフライティング時に、良性の初期化エラーがフィルターで除外されます
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 1e4bbe42d603b3b95b2c0f58ed4c9f8deeffdfb0
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "71017070"
---
# <a name="firmware-measures"></a>ファームウェアの測定値

Windows では、ドライバー パッケージを通じてマシンおよびデバイスのファームウェア更新プログラムをインストールするプラットフォームをサポートしています。これらのドライバー パッケージは「[Windows UEFI ファームウェア更新プラットフォーム](https://docs.microsoft.com/windows-hardware/drivers/bringup/windows-uefi-firmware-update-platform)」に説明があるとおり、UEFI 更新カプセル機能を使用して処理されます。 UEFI プラットフォームでは、マシンとデバイス両方のレベルのファームウェア更新がサポートされており、外部パートナーは顧客のマシンを安全に更新することができます。 ファームウェア パッケージに問題がある場合、ユーザーのマシンに深刻な悪影響が及び、マシンがまったく機能しなくなる可能性があります。
