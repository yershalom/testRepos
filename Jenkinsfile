node() {
  checkout scm
  def repo = scm.getUserRemoteConfigs()[0].getUrl().tokenize('/').last().split("\\.")[0]
  println(repo)
}
