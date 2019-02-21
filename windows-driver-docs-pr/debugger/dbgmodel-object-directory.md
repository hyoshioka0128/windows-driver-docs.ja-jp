---
title: デバッガーのデータ モデル - ディレクトリ オブジェクト
description: ディレクトリ オブジェクトを表し、ファイル システム上のディレクトリを操作します。
ms.date: 12/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: c6ef217cee7a0cc28fd803e7e32ae2fd0249b46c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538659"
---
# <a name="directory-objects"></a>ディレクトリ オブジェクト 
## <a name="summary"></a>概要
ディレクトリ オブジェクトを表し、ファイル システム上のディレクトリを操作します。

## <a name="object-methods"></a>オブジェクトのメソッド
|名前|戻り値の型|署名|説明|
|--- |-- |--- |--- |
|CreateFile|[ファイル](dbgmodel-object-file.md)|CreateFile (relativePath、[破棄])|特定のディス ポジションをディレクトリ内のファイルを作成します。 破棄は"OpenExisting"、"CreateNew"または"CreateAlways"のいずれかの可能性があります。|
|CreateSubDirectory|[directory](dbgmodel-object-directory.md)|CreateSubDirectory(name)|ディレクトリ内の新しいサブディレクトリを作成します。|
|削除||Delete()|空の場合は、サブディレクトリを削除します。|
|OpenFile|[ファイル](dbgmodel-object-file.md)|OpenFile(relativePath)|ディレクトリからの読み取り用の既存のファイルを開きます。|


## <a name="object-properties"></a>オブジェクトのプロパティ
|名前|説明|
|--- |--- |
|ファイル|A[コレクション](dbgmodel-namespace-collections.md)の[ファイル](dbgmodel-object-file.md)ディレクトリ内で。|
|サブディレクトリ|A[コレクション](dbgmodel-namespace-collections.md)の[ディレクトリ](dbgmodel-object-directory.md)ディレクトリ内で。|