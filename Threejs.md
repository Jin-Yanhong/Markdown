## 扩散波特效

```javascript
let texture = new THREE.TextureLoader().load("ball.png")
  texture.wrapS = texture.wrapT = THREE.RepeatWrapping; //每个都重复
  texture.repeat.set(1, 1)
  texture.needsUpdate = true


  let geometry = new THREE.CylinderGeometry(4, 4, 2, 64);
  let materials = [
    new THREE.MeshBasicMaterial({
      map: texture,
      side: THREE.DoubleSide,
      transparent: true
    }),
    new THREE.MeshBasicMaterial({
      transparent: true,
      opacity: 0,
      side: THREE.DoubleSide
    }),
    new THREE.MeshBasicMaterial({
      transparent: true,
      opacity: 0,
      side: THREE.DoubleSide
    })
  ]
  let mesh = new THREE.Mesh(geometry, materials)

  scene.add(mesh)

  let s = 0;
  let p = 1;
  function animate() {
	// 一定要在此函数中调用
    s += 0.01;
    p -= 0.005;
    if (s > 2) {
      s = 0;
      p = 1;
    }
    mesh.scale.set(1 + s, 1, 1 + s);
    mesh.material[0].opacity = p;
    
    requestAnimationFrame(animate)
  }

  animate()
```

