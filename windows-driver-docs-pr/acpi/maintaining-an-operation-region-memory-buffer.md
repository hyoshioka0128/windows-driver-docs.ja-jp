---
title: 操作領域のメモリ バッファーを維持する
description: 操作領域のメモリ バッファーを維持する
ms.assetid: 4abe82ec-d8c4-43c1-a72f-5114ba07160e
keywords:
- ACPI デバイス WDK、操作リージョン
- 操作リージョン WDK ACPI
- 関数ドライバー WDK ACPI、操作リージョン
- WDM 関数ドライバー WDK ACPI、操作リージョン
- 操作領域のメモリバッファーの WDK ACPI
- メモリバッファー WDK ACPI
ms.date: 05/19/2020
ms.localizationpriority: medium
ms.openlocfilehash: 79ce8e07cc5a005a798e87d08db3d8dfb812d039
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769336"
---
# <a name="maintaining-an-operation-region-memory-buffer"></a>操作領域のメモリ バッファーを維持する

このドライバーは、操作領域のメモリバッファーを保持します。 メモリバッファーには、操作領域に関連付けられたデータフィールドが格納されます。 ACPI ドライバーは、操作領域のメモリバッファー内のデータフィールドにアクセスするために、操作領域ハンドラーを呼び出します。

操作領域のメモリバッファーは、次のものに準拠している必要があります。

- メモリバッファーは、非ページングシステムメモリから割り当てられる必要があります。

- バッファーサイズは、ACPI デバイス用に定義されている操作領域のサイズ以上である必要があります。

- ドライバーがアクセスする操作領域ハンドラーを登録する前に、バッファーを割り当てる必要があります。また、ハンドラーが登録されている間は保持されます。

操作領域の制約の詳細については、「[高度な構成と電源インターフェイスの仕様](https://uefi.org/specifications)」を参照してください。
