pkgdesc="ROS - Common-Lisp ROS message and service generators."
url='http://www.ros.org/'

pkgname='ros-groovy-genlisp'
pkgver='0.4.10'
arch=('i686' 'x86_64')
pkgrel=1
license=('BSD')
makedepends=('ros-build-tools')

depends=(ros-groovy-catkin
  ros-groovy-genmsg)

build() {
  [ -f /opt/ros/groovy/setup.bash ] && source /opt/ros/groovy/setup.bash
  if [ -d ${srcdir}/genlisp ]; then
    cd ${srcdir}/genlisp
    git fetch origin --tags
    git reset --hard release/genlisp/${pkgver}
  else
    git clone -b release/genlisp/${pkgver} git://github.com/ros-gbp/genlisp-release.git ${srcdir}/genlisp
  fi
  [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
  cd ${srcdir}/build
  /usr/share/ros-build-tools/fix-python-scripts.sh ${srcdir}/genlisp
  cmake ${srcdir}/genlisp -DCATKIN_BUILD_BINARY_PACKAGE=ON -DCMAKE_INSTALL_PREFIX=/opt/ros/groovy -DPYTHON_EXECUTABLE=/usr/bin/python2 -DPYTHON_INCLUDE_DIR=/usr/include/python2.7 -DPYTHON_LIBRARY=/usr/lib/libpython2.7.so -DSETUPTOOLS_DEB_LAYOUT=OFF
  make
}

package() {
  cd "${srcdir}/build"
  make DESTDIR="${pkgdir}/" install
}
