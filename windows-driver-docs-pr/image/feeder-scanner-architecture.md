---
title: フィーダー スキャナーのアーキテクチャ
description: フィーダー スキャナーのアーキテクチャ
ms.assetid: 02157a88-fccd-4a23-a4ee-174755c8d3aa
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4cab56f84b9053530b82c669ca4457615d4cb6bf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573239"
---
# <a name="feeder-scanner-architecture"></a>フィーダー スキャナーのアーキテクチャ





ドキュメント フィーダーの単位がスキャナーのデバイスはドキュメント フィーダーに配置されているドキュメントから生成する場合は、イメージ、WIA 項目のツリーで、フィーダー項目を実装する必要があります。 フィーダー項目は、プログラミング可能なデータ ソースを表すし、スキャナーのドキュメント フィーダー付きのデータ転送はこの項目から要求されたときにユニットのスキャンに配置されているドキュメントからイメージを生成します。 スキャナーのフィーダー項目では、WIA ルート項目から直接配置して、前面を表し、ドキュメントのページをバックアップする 1 つまたは複数の子項目を含めることができます。

次のトピックでは、ドキュメント フィーダー付きのスキャンをサポートするフラット ベッド スキャナーの例について説明します。

[二重モード対応のドキュメント フィーダー付き](non-duplex-capable-document-feeder.md)

[単純な二重モード対応ドキュメント フィーダー](simple-duplex-capable-document-feeder.md)

[二重モード対応の高度なドキュメント フィーダー](advanced-duplex-capable-document-feeder.md)

 

 




