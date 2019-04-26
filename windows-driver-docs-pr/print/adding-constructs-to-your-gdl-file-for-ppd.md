---
title: PPD の GDL ファイルにコンストラクトを追加する
description: PPD の GDL ファイルにコンストラクトを追加する
ms.assetid: 981952b2-cc13-4c62-935b-74e749278c0f
keywords:
- WDK プリンター autoconfig を構築します。
- PPD ファイル WDK の自動構成を構築します
- ボックスの自動構成サポート WDK プリンター、コンストラクト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30b89bc0f78ffcca00337410f1144a2c7d43e924
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343232"
---
# <a name="adding-constructs-to-your-gdl-file-for-ppd"></a>PPD の GDL ファイルにコンストラクトを追加する


自動構成をサポートするには、次の新しいキーワードを使用して GDL ファイルに構造を追加する必要があります。\***BidiQuery**、 \* **QueryString**、 \* **BidiResponse**、 \* **ResponseType**、 \* **ResponseData**、および\* **BidiValue**します。 これらのキーワードを使用して、機能とそのオプションに選択肢の 1 つのオプションに関連付けられている bidi スキーマの要求を指定することができます。

A \***機能**コンス トラクターは、1 つを含めることができます\* **BidiQuery**のコンテナーとして機能する、構築、 \* **QueryString**インスタンス。 クエリ文字列を\***機能**コンス トラクターのインスタンスが照会される追加機能への双方向通信スキーマ パスの特定のプロパティの名前で構成される Unicode 文字列、機能です。

A \***機能**コンストラクトでは、1 つを含めることができますも\* **BidiResponse**コンス トラクターは、1 つのコンテナーとして機能する\* **ResponseType**インスタンスと省略可能な\* **ResponseData**インスタンス。

各\***オプション**コンストラクトに関連付けられている、 \***機能**コンス トラクターを含める必要があります、 \* **BidiValue**インスタンス適切な応答の文字列表現を含む\***オプション**します。

次の例では、適切な構成要素を PPD ファイルに示す機能に基づいて、GDL ファイルに追加する方法を示します。 最初の 2 つの例は、PPD サンプルと GDL サンプルの自動検出または特定のインストール可能な機能の自動構成をサポートするために必要な構成要素で構成されます。 3 番目の例では、GDL サンプルは、ハード ドライブの自動検出とのハード ドライブの PPD 特徴の定義が存在することを前提としています。

[Autodetect PPD の両面印刷ユニット](autodetect-the-duplex-unit-for-ppd.md)

[自動構成 PPD のプリンターのメモリ](autoconfigure-the-printer-s-memory-for-ppd.md)

[Autodetect、プリンターのハード ドライブ PPD](autodetect-the-printer-s-hard-drive-for-ppd.md)

 

 




