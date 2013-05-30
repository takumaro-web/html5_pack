////////////////////////////////////////////////////////////////////
html5_package with grunt.js
Windows���pbat�t�@�C���t

update 2013.05.14
tsukasa-oneslocus
https://github.com/tsukasa-oneslocus
////////////////////////////////////////////////////////////////////

--------------------------------------------------------------------
�T�v
--------------------------------------------------------------------
�ȒP��grunt.js�̐ݒ�E�N�����ł���t�@�C���ꎮ�ł��B
Gruntfile.js��ύX���邱�ƂŐݒ�̕ύX��f�B���N�g���̕ύX���\�ł��B

--------------------------------------------------------------------
�@�\
--------------------------------------------------------------------
�ECoffeeScript�̃R���p�C��
�ESass�̃R���p�C��
�Ecss/js�t�@�C���̌��������k
�EjsHint�ɂ��f�o�b�O
�Ewatch�ɂ��t�@�C���X�V�̊Ď����R���p�C���E�����E���k�E�f�o�b�O�̎�����
�E�����u���E�U�����[�h

--------------------------------------------------------------------
������
--------------------------------------------------------------------
���O�̒m�������Ƀf�B���N�g���\����ύX����ƁA�܂������Ȃ��Ǝv���Ă��������đ��v�ł��B
bat�t�@�C����package.json��Gruntfile.js���K��docs�����Œu���悤�ɂ��Ă��������B

���v���O�C�����̒��쌠�L�q���K�v��js�t�@�C���̓R�����g�̃��C�Z���X�\�L�̑O�ɕK��@license���L�q���Ă��������B
������L�q���邱�Ƃň��k���Ƀ��C�Z���X�L�q�R�����g�̂ݎc��悤�ɂȂ�܂��B

�i��F
/* @license
 * Bootstrap.js by @fat & @mdo
 *
 * plugins: bootstrap-transition.js, bootstrap-dropdown.js, bootstrap-carousel.js
 * Copyright 2012 Twitter, Inc.
 * http://www.apache.org/licenses/LICENSE-2.0.txt
 */

--------------------------------------------------------------------
�ݒ�菇
--------------------------------------------------------------------
�����Ԃ�K�����܂��傤�B

�@Node.js���C���X�g�[��
http://nodejs.org/

�Agrunt���C���X�g�[��
Windows�́A�L�[�{�[�h�� [win]+[r]�������āA�u�t�@�C�������w�肵�Ď��s�v�� cmd ����́B
�R�}���h�v�����v�g���N������͂��ł��B
�N�������炷������
-----------------------------
npm install -g grunt-cli
-----------------------------
�Ɠ��͂���grunt���C���X�g�[�����Ă��������B
�Ǘ��������ŃG���[���o���l�͊Ǘ��Ҍ�����cmd���N�����Ă��������B


�B�f�B���N�g���쐬
�p�b�P�[�W���ɓ����Ă���docs���f�B���N�g�����ɔz�u���܂��Bdocs��root�ł��B
���łɃf�B���N�g�����쐬�ς݂̏ꍇ�́A�p�b�P�[�W���̃f�B���N�g���Ɠ����ɂȂ�悤�Ƀ}�[�W���Ă��������B
�f�B���N�g���̐����ɂ��Ă̓p�b�P�[�W����ppt���Q�Ƃ��Ă��������B

��Compass�ɂ��āiSass���g��Ȃ��l�͓ǂݔ�΂��Ă��������đ��v�ł��j
------------------------------------------------------------------
Compass���̂͒ʏ�ʂ�@import "compass";�Ŏg���܂��B
Compass�̃C���[�W�f�B���N�g����/common/images/�ɐݒ肳��Ă��܂��B
���̂��߁A�X�v���C�g�V�[�g�̃C���|�[�g�̓f�B���N�g���ʂ�ɂ����
@import "sprite/*.png";�ɂȂ�܂��B


�C�v���O�C���̃C���X�g�[��
root������grunt_install.bat��@���Ă��������B
�v���O�C�����̃C���X�g�[�����n�܂�܂��Bnode_modules�������ɐ��������͂��ł��B


�DGruntfile.js�̒���

CoffeeScript���g���l�͕K��js�̏o�͖����L�q���Ă��������B
top-level��function�ŕ����������option�̕����������Ă��������B

/* coffee�X�N���v�g�̃R���p�C��
------------------------------------------------------------------------*/
coffee: {
	compile: {
		//top-level��function��t����������option�������Ă��������B
		options: {
      			bare: true
    		},
		files:{
			//coffee����js�ɏo�͂���ۂ̃t�@�C�����w�肪�K�v�ł��B
			'common/js/hogehoge.js': ['compile/*.coffee']
		}
	}
},
//-----------------------------------------------------------------------

Gruntfile.js���J���A����������css,js�̃p�X��ʂ��܂��B
�ォ�珇�Ɍ�������Ă����̂ŁA���Ԃ��ԈႦ�Ȃ��悤�ɂ��Ă��������B
���Ȃ݂�Grunt.js�ɂ����ă��[�g���΁E��΃p�X�͔F������܂���B

/* js,css�t�@�C���̌���
------------------------------------------------------------------------*/
concat: {
	style: {
		src: [
			'common/css/hogehoge.css',
			'common/css/hogehoge2.css',
			'common/css/hogehoge3.css'
		],
		dest: 'common/all/style-all.css'
	},
	run: {
		src: [
			'common/js/hogehoge.js',
			'common/js/hogehoge2.js',
			'common/js/hogehoge3.js',
			'common/js/hogehoge4.js'
		],
		dest: 'common/all/run-all.js'
	}
},
//-----------------------------------------------------------------------


�E�^�X�N�𑖂点��
�������łɐ��삪�i��ł����Ԃ�scss/css/coffee/js���쐬����Ă���ꍇ�́A
�t�@�C�����f�B���N�g���ʂ�ɔz�u����Ă��邩���m�F����������grunt_command.bat��@���Ă��������B
��x�R���p�C���E�����E���k�E�f�o�b�O���s���܂��B
/common/all/�z���Ɍ������ꂽcss/js�t�@�C���������Ă���ΐ����ł��B


�F�t�@�C���Ď����N��
�@�`�E���I������珀�������ł��Bgrunt_watch.bat��grunt_livereload��@���Ă��������B
Sublime Text2��livereload�̃v���O�C�������Ă�l�́A�o�b�e�B���O����̂Ńv���O�C����remove���Ă���g���Ă��������B
���̌�A�R���\�[���͏o�����܂܂ɂ��Ă����Ă��������B�ŏ������Ă����v�ł��B
�ȍ~��scss/css/coffee/js���X�V�����x�Ɏ����I�ɃR���p�C���E�����E���k�E�f�o�b�O���s���܂��B
����ɁAhtml��css(sass���g���Ă���l��scss�X�V��)�̍X�V���Ɏ����Ńu���E�U�������[�h����܂��B
�R���\�[���͏������ɏo�����܂܂ɂ��Ă����Ă��������B�Ď�����߂����ꍇ�̓R���\�[�����Ctrl+C�������Ă��������B
�C�ӂ̃^�C�~���O�ŃR���p�C���E�����E���k�E�f�o�b�O���s�������ꍇ��grunt_command.bat��@�����A
�R���\�[����Ługrunt�v�Ƒł�����ł��������B


�GSVN����ݒ�t�@�C�������O����
���|�W�g������e��ݒ�t�@�C�������O���܂��B
�u�E�N���b�N��TortoiseSVN���o�[�W�����Ǘ����珜�O���A�������X�g�ɒǉ��v
�Epackage.json
�EGruntfile.js
�Egrunt_command.bat
�Egrunt_install.bat
�Egrunt_watch.bat
�Egrunt_livereload.bat
�Enode_modules�t�H���_
�E.sass-cache�t�H���_�iSass�g�p�҂̂݁j

�Hfirefox�܂���chrome�Ɏ��������[�h�p�̃A�h�I��or�G�N�X�e���V����������

Firefox
http://feedback.livereload.com/knowledgebase/articles/86242-how-do-i-install-and-use-the-browser-extensions-
�uFirefox extension�v�Ƃ�����ł��B

Chrome
https://chrome.google.com/webstore/detail/livereload/jnihajbhpnppcggbcgedagnkighmdlei

���Ƃ͒ǉ����ꂽ�A�h�I���̃}�[�N�������āA�ۂ̒����Ԃ��Ȃ�ΐ����ł��B
���html�܂���css(sass�̐l��scss)��ҏW���ĕۑ������ۂɃu���E�U�������[�h������ok�B

�H�ʂ̈Č��Ŏg���Ƃ���
�B�`�G���J��Ԃ��Α��v�ł��B
