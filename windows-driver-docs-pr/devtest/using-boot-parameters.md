---
title: ブート パラメーターの使用
description: ブート パラメーターの使用
ms.assetid: f249f312-cfc5-41b2-ad67-75497a929e35
keywords:
- ブートエントリ WDK
- ブートオプション WDK、ブートパラメーター
- WDK ブートオプションのドライバーテスト
- ドライバーのテスト WDK ブートオプション
- デバッグドライバーの WDK ブートオプション
- ドライバーのデバッグ WDK ブートオプション
- NVRAM ブートオプション WDK、ブートパラメーター
- EFI NVRAM ブートオプション WDK、ブートパラメーター
- Boot.ini ファイルの WDK、ブートパラメーター
ms.date: 06/04/2020
ms.localizationpriority: medium
ms.openlocfilehash: 893aacd257d1333bf1163d5f34faf388c3c1330d
ms.sourcegitcommit: 0a0b75d93130b6c5854279607cd0aac099f65fd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84428345"
---
# <a name="using-boot-parameters"></a>ブートパラメーターの使用

多くの場合、ドライバーの開発者とテスト担当者は、変数の条件に基づいてドライバーをテストするために、ブートエントリのパラメーターを追加、削除、変更する必要があります。 このセクションでは、いくつかの一般的なシナリオについて説明し、boot.ini ファイルと NVRAM でブートパラメーターを構成するための方法を提案します。

> [!NOTE]
> チェックを行ったビルドは、Windows 10 バージョン1803より前の古いバージョンの Windows で使用できました。
> Driver Verifier や GFlags などのツールを使用して、新しいバージョンの Windows でドライバーコードを確認します。

このセクションでは、以下のトピックについて説明します。

[デバッグを有効にするためのブート パラメーター](boot-parameters-to-enable-debugging.md)

[メモリを操作するためのブート パラメーター](boot-parameters-to-manipulate-memory.md)

[部分チェック ビルドを読み込むためのブート パラメーター](boot-parameters-to-load-a-partial-checked-build.md)

[EMS リダイレクトを有効にするためのブート パラメーター](boot-parameters-to-enable-ems-redirection.md)

[DEP と PAE を構成するためのブート パラメーター](boot-parameters-to-configure-dep-and-pae.md)
