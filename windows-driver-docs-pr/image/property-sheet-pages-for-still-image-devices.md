---
title: 静止画像デバイスのプロパティ シート
description: 静止画像デバイスのプロパティ シート
ms.assetid: ef77e57d-f791-4afa-8d51-67e78b60cf57
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c459ae18b2b3ae6788c1e5462516d7eb6189e8e1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379640"
---
# <a name="property-sheet-pages-for-still-image-devices"></a>静止画像デバイスのプロパティ シート





デバイス固有のプロパティ シートのページを作成する DLL を行うことができます。 スキャナーとカメラのコントロール パネルは、ユーザーがデバイスのプロパティ シートを表示しようとした場合、DLL のエントリ ポイントを呼び出します。

インストールして使用するには、この DLL を含める必要があります、**プロパティ ページ**セットアップ情報 (INF) ファイル内のエントリ。 このエントリには、DLL のファイル名とエントリ ポイント名が含まれています。 詳細については、次を参照してください。[静止画像デバイスの INF ファイル](inf-files-for-still-image-devices.md)します。

 

 




