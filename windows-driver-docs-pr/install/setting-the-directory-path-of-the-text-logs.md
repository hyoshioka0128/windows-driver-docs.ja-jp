---
title: テキスト ログのディレクトリ パスの設定
description: テキスト ログのディレクトリ パスの設定
ms.assetid: d56a8f6c-365b-427d-b965-65616ede3d7e
keywords:
- テキスト ログの WDK SetupAPI、ディレクトリのパス
- ディレクトリ パスの WDK SetupAPI ログ
- LogPath
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f923094189d30b9515fde20843eb624102e2d8b3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578137"
---
# <a name="setting-the-directory-path-of-the-text-logs"></a>テキスト ログのディレクトリ パスの設定


既定では、SetupAPI テキスト ログが Windows のシステム ディレクトリにあります。 SetupAPI テキスト ログの場所は、次を設定して変更できます[REG_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)レジストリ値。

**HKEY_LOCAL_MACHINE\\ソフトウェア\\Microsoft\\Windows\\CurrentVersion\\セットアップ\\LogPath**

**LogPath**レジストリ値は、ディレクトリの完全修飾パスである必要があります。 パスが存在する必要があり、パスは、ファイル名を含めることはできません。

場合、 **LogPath**レジストリ値が存在しない、パスが存在しないかパスにはファイル名が含まれています、SetupAPI でテキスト ログの検索、 *%SystemRoot%/Inf*ディレクトリ。

 

 





