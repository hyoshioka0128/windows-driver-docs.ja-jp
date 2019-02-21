---
title: PPD スキーマの新しいキーワード
description: PPD スキーマの新しいキーワード
ms.assetid: 05caa402-4949-4c0f-913c-1c87e65c30d7
keywords:
- ルート レベルのキーワードの WDK プリンターの自動構成
- PPD ファイル WDK 自動構成、キーワード
- キーワードの WDK プリンターの自動構成
- ボックスの自動構成サポート WDK プリンター、キーワード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aca48475ae56745bb52cd7decd34bfecc9b64b7c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529231"
---
# <a name="ew-keyword-for-ppd-schema"></a>PPD スキーマの新しいキーワード


Windows Vista と Windows の以降のバージョンでは、新しいルート レベルのキーワードを PPD で GDL ファイルを指す PPD ファイルに追加する必要があります\* **MSBidiQueryFile**、bidi を含む GDL ファイルを識別する場合自動構成に必要な対応付け情報。 キーワードが不足している場合、AutoConfig が GDL パーサーを呼び出す GDL ファイルを検索するには、もう一度、ファイル システムをヒットしたり必要はありません。

PScript ベースのドライバーは、個別 GDL を使用する必要がありますを記述する開発者ファイルをドライバーの主な PPD ファイル参照を使用して直接、 \* **MSBidiQueryFile**キーワード。

 

 




