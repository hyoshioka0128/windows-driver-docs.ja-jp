---
title: Debugger Data Model - ファイル オブジェクト
description: ファイル オブジェクトは、開く、編集、およびそれ以外の場合、ファイル システム上のファイルの操作に使用されます。
ms.date: 12/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: eb3f164e08775bfac769ba0edfd24f5056c2748d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376084"
---
# <a name="file-objects"></a>ファイル オブジェクト 
## <a name="summary"></a>概要
ファイル オブジェクトは、開く、編集、およびそれ以外の場合、ファイル システム上のファイルの操作に使用されます。

## <a name="object-methods"></a>オブジェクトのメソッド
|名前|戻り値の型|署名|説明|
|--- |--- |--- |--- |
|Close||Close()|ファイルを閉じます。 |
|DELETE||Delete()|ファイルを削除します|
|[ファイル]||Open(disposition)|ファイルを開き、指定された*廃棄*します。 *廃棄*"OpenExisting"、"CreateNew"または"CreateAlways"のいずれかを指定することがあります。|
|ReadBytes|バイトの配列|ReadBytes(byteCount)|ファイルから指定したバイト数を読み取り、それらのバイトのインデックスを付けると、反復可能な配列を返します。|
|WriteBytes||WriteBytes(bytes, [byteCount])|指定したバイトをファイルに書き込みます。 場合*byteCount*が指定されていないの反復処理できるすべてのバイト*バイト*それ以外のファイルに書き込まれた最初の*byteCount*内のバイト *。バイト*が書き込まれます。|

## <a name="object-properties"></a>オブジェクトのプロパティ
|名前|説明|
|--- |--- |
|拡張|ファイル拡張子を含む文字列。|
|名前|ファイルの名前を含む文字列。|
|パス|ファイルへの完全修飾パスを含む文字列。|
|位置|ファイル内の現在の読み取り/書き込みカーソルの位置。|
|サイズ|ファイルのサイズ (バイト単位)。|

## <a name="remarks"></a>注釈
JavaScript スクリプトなどのガベージ収集環境からのファイルを使用している場合とではありませんが、ファイルを閉じるガベージ コレクションを待機するのではなく、使用閉じる必要があります。
