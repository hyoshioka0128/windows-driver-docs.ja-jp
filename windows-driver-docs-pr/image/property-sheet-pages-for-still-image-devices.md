---
title: 静止画像デバイスのプロパティ シート
description: 静止画像デバイスのプロパティ シート
ms.assetid: ef77e57d-f791-4afa-8d51-67e78b60cf57
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c459ae18b2b3ae6788c1e5462516d7eb6189e8e1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572065"
---
# <a name="property-sheet-pages-for-still-image-devices"></a>静止画像デバイスのプロパティ シート





デバイス固有のプロパティ シートのページを作成する DLL を行うことができます。 スキャナーとカメラのコントロール パネルは、ユーザーがデバイスのプロパティ シートを表示しようとした場合、DLL のエントリ ポイントを呼び出します。

インストールして使用するには、この DLL を含める必要があります、**プロパティ ページ**セットアップ情報 (INF) ファイル内のエントリ。 このエントリには、DLL のファイル名とエントリ ポイント名が含まれています。 詳細については、[静止画像デバイスの INF ファイル](inf-files-for-still-image-devices.md)を参照してください。

 

 




