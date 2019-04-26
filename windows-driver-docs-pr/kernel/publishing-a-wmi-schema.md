---
title: WMI スキーマの公開
description: WMI スキーマの公開
ms.assetid: db2b8086-71e4-4532-a0ae-75983691a5a6
keywords:
- WMI の WDK カーネルでは、スキーマの公開
- 発行の WMI スキーマ WDK
- 発行 WDK WMI スキーマ
- MOF ファイルの WDK WMI
- バイナリの MOF WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8044412f723b88d6aea21518cf950e894a51ab33
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338503"
---
# <a name="publishing-a-wmi-schema"></a>WMI スキーマの公開





WMI スキーマを発行するドライバー ライターまずテキスト ファイルを作成データのブロックと、スキーマ内のイベントのブロックごとにクラス定義を含む管理オブジェクト フォーマット (MOF) の言語で」の説明に従って[WMI データとイベント ブロックMOF構文](mof-syntax-for-wmi-data-and-event-blocks.md).

ドライバー開発者は、次の方法のいずれかでドライバーの WMI スキーマを発行できます。

-   MOF ファイルをコンパイルし、ドライバーのバイナリ イメージのリソースとして含めます。 詳細については、次を参照してください。[ドライバーの MOF ファイルをコンパイルする](compiling-a-driver-s-mof-file.md)します。

-   DLL などの別のファイルにリソースとしてコンパイル済みの MOF ファイルを含めるし、レジストリ値を追加**MofImagePath**ドライバーのサービス キーの下の MOF を含むファイルへのパスを使用します。 この方法で公開されるスキーマは、ドライバーを再コンパイルしなくても更新できます。 詳細については、次を参照してください。 [MofImagePath レジストリ値を設定](setting-the-mofimagepath-registry-value.md)します。

-   ドライバー内でバイナリ データを含めるし、WMI の要求時に返すことです。 この方法で公開されるスキーマは、実行時に動的に変更することができます。 詳細については、次を参照してください。[動的 MOF データを実装する](implementing-dynamic-mof-data.md)します。

 

 




