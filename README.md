passwordhash-ci
===============

PasswordHash with sensible defaults, primarily for use in CodeIgniter projects

Drop it into your application/libraries folder.

Example use for checking a user login:

        $this->load->library( 'PasswordHash' );

		$query = $this->db->query("
			SELECT
				`user_id`,`password` AS `hash`
			FROM
				`user`
			WHERE	
				`username` = ". $this->db->escape($username) ."
			LIMIT
				1
		");
		
        // check to see whether username exists
        if ( $query->num_rows() == 1 ) {
			$row = $query->row();

            if ( $this->passwordhash->CheckPassword( $password, $row->hash ) ) {
                return $row->user_id;
            }
        }


Example use for creating a hashed password:

        $this->load->library( 'PasswordHash' );

        $password = ( isset( $_POST['password'] ) ? $_POST['password'] : '' );

        if ( $password ) {
            $hash = $this->passwordhash->HashPassword( $password );

            if ( strlen( $hash ) < 20 ) {
                exit( "Failed to hash new password" );
            }
        }
