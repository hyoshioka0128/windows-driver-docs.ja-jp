---
title: 使用不可のブート エントリのバックアップ ファイルを認識します。
description: 使用不可のブート エントリのバックアップ ファイルを認識します。
ms.assetid: ff61c8e9-ad6b-4f3f-9c4b-72c24c27eda6
keywords:
- NVRAM ブート オプション WDK、
- EFI NVRAM ブート オプション WDK、
ms.date: 07/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: e84f7deda6ff41901cbae59ef00ec3872886f77c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532150"
---
# <a name="recognizing-unusable-boot-entry-backup-files"></a>使用不可のブート エントリのバックアップ ファイルを認識します。

残念ながら、ブート エントリのバックアップ コピーは常に使用できません。

EFI 環境では、アプリケーションとドライバーは、パーティション GUID によってディスク パーティションを識別します。 何らかの理由で、ディスク パーティションの GUID が変更された場合は、ブート エントリのバックアップ コピーでは、パーティション GUID は無効になりましたし、EFI ブート ローダーは、バックアップのコピーを使用して、システムを起動することはできません。

次の Bootcfg は、無効なパーティションの Guid を持つインポートされたブート エントリを示しています。

```
Boot entry ID:    4
OS Friendly Name: Windows Server 2003 - mydebug
OsLoadOptions:    /debug /debugport=com1 /baudrate=115200
BootFilePath:     (null)
OsFilePath:       (null)
```

ここでは、オペレーティング システムのインストールから別のブート エントリをコピーして、パラメーターを変更するブート エントリを再作成する必要があります。
