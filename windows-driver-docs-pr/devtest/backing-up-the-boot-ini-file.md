---
title: Boot.ini ファイルをバックアップします。
description: インストールまたは Windows Vista より前に、NT ベースの Windows オペレーティング システムをアップグレードするとき、Windows インストーラーは、コンピューターの新しい Boot.ini ファイルを作成します。 新しいファイルは、ファイルに加えた可能性がありますが、変更のすべてではなく、一部を保持します。
ms.assetid: c4881f5d-3404-4e87-b130-33bc57b45ec9
keywords:
- Boot.ini ファイルをバックアップする WDK
- 戻る ups の WDK ブート オプション
- 戻る ups の WDK のブート オプション、Boot.ini ファイル
- コピーのブート オプション
- ブート オプションを保存しています
- ブート オプション WDK、バックアップします。
ms.date: 07/03/2018
ms.localizationpriority: medium
ms.openlocfilehash: 467b034145356b8bd5ea429c1a9ac27f9f6ae2a1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536949"
---
# <a name="backing-up-the-bootini-file"></a>Boot.ini ファイルをバックアップします。


> [!IMPORTANT] 
> このトピックでは、Windows XP および Windows Server 2003 でサポートされるブート オプションについて説明します。 Windows の最新バージョンのブート オプションを変更する場合は、[Windows Vista 以降のブート オプション](boot-options-in-windows-vista-and-later.md)を参照してください。

Windows インストーラーを作成し、新しいインストールは以前に比べて Windows XP、Windows Server 2003、またはそのいずれかにアップグレードすると、 *Boot.ini*コンピューターのファイル。 新しいファイルは、ファイルに加えた可能性がありますが、変更のすべてではなく、一部を保持します。 そのため、編集、保持するために*Boot.ini*ファイルで、オペレーティング システムをインストールまたはアップグレードする前にバックアップ コピーを作成します。 更新プログラムが完了すると、バックアップ コピーを使用して、新しいファイルを変更できます。 新しいオペレーティング システムをインストールした場合、バックアップ コピーからカスタマイズされたエントリをコピーし、新しいに貼り付けます*Boot.ini*ファイル。

更新プログラムまたはインストールは、読み取り専用属性を含む、Boot.ini で既定のセキュリティ属性を復元します。 ファイルを編集するには、Bootcfg コマンドを使用するか、ファイル属性を変更します。 詳細については、[Boot.ini ファイルの編集](editing-the-boot-ini-file.md)を参照してください。


