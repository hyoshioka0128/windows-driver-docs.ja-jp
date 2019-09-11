---
title: ファームウェアの測定値
description: ファームウェアの測定値では、ファームウェア ドライバーのフライティング時に、良性の初期化エラーがフィルターで除外されます
ms.topic: article
ms.date: 05/20/2019
ms.author: paslote
author: parkeratmicrosoft
ms.localizationpriority: medium
ms.openlocfilehash: db5188e72ef73559714a579ae98b2a304046d71c
ms.sourcegitcommit: 04da1962e34908adeca54fcf5bbfbaa456efca5f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/03/2019
ms.locfileid: "70224024"
---
# <a name="firmware-measures"></a>ファームウェアの測定値

Windows では、ドライバー パッケージを通じてマシンおよびデバイスのファームウェア更新プログラムをインストールするプラットフォームをサポートしています。これらのドライバー パッケージは「[Windows UEFI ファームウェア更新プラットフォーム](https://docs.microsoft.com/windows-hardware/drivers/bringup/windows-uefi-firmware-update-platform)」に説明があるとおり、UEFI 更新カプセル機能を使用して処理されます。 UEFI プラットフォームでは、マシンとデバイス両方のレベルのファームウェア更新がサポートされており、外部パートナーは顧客のマシンを安全に更新することができます。 ファームウェア パッケージに問題がある場合、ユーザーのマシンに深刻な悪影響が及び、マシンがまったく機能しなくなる可能性があります。
