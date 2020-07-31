---
title: SymStore の圧縮ファイル
description: SymStore の圧縮ファイル
ms.assetid: 4ec6a7f5-ceee-46d5-9a5e-36ab9fe9db52
keywords:
- SymStore、圧縮ファイル
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6244d1b7a0fefcc4d0e0db4e42028504e540f4f5
ms.sourcegitcommit: 1d531bf9d02653fdf9ad728126d68b8acb86182e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2020
ms.locfileid: "87402265"
---
# <a name="symstore-compressed-files"></a>SymStore の圧縮ファイル

SymStore は、次の2つの方法で圧縮ファイルと共に使用できます。

1. SymStore を **/p**オプションと共に使用して、シンボルファイルへのポインターを格納します。 SymStore が完了したら、ポインターが参照するファイルを圧縮します。

2. SymStore を **/x**オプションと共に使用して、インデックスファイルを作成します。 SymStore が完了したら、インデックスファイルに示されているファイルを圧縮します。 次に、SymStore を **/y**オプションと共に使用し (必要に応じて **/p**オプションを使用して)、ファイルまたはポインターをシンボルストアに格納します。 (SymStore は、この操作を実行するためにファイルを圧縮解除する必要はありません)。

シンボルサーバーは、適切なタイミングでファイルの圧縮を解除します。

シンボルサーバーとして SymSrv を使用している場合は、 [Microsoft ダウンロードセンター](https://www.microsoft.com/download/details.aspx?displaylang=en&id=17657)から入手できる compress.exe ツールを使用して圧縮を行う必要があります。 圧縮ファイルには、ファイル拡張子の最後の文字としてアンダースコア (たとえば、 \_ module2 または) を指定する必要があり \_ ます。 詳細については、「 [Symsrv](symsrv.md)」を参照してください。
